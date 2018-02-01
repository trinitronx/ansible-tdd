# A sample Guardfile
# More info at https://github.com/guard/guard#readme

## Uncomment and set this to only include directories you want to watch
# directories %w(app lib config test spec features) \
#  .select{|d| Dir.exists?(d) ? d : UI.warning("Directory #{d} does not exist")}

## Note: if you are using the `directories` clause above and you are not
## watching the project directory ('.'), then you will want to move
## the Guardfile to a watched dir and symlink it back, e.g.
#
#  $ mkdir config
#  $ mv Guardfile config/
#  $ ln -s config/Guardfile .
#
# and, you'll have to watch "config/Guardfile" instead of "Guardfile"

guard :yaml do
  watch(%r{^playbooks/(.*)/(.*)\.yml$})
  watch(%r{^roles/(.*)/(.*)\.yml$})
end

guard :shell do
  # watch /.*/ do |m|
  #   n m[0], 'File Changed'
  # end
  watch( /^playbooks\/([^\/]+)\/([^\/]*)\.yml$/ ) do |m|
    if File.exists?(File.join( "#{ENV['HOME']}", 'secrets', "ansible-vault-#{m[1]}" ))
      ansible_vault_password_file = File.join( "#{ENV['HOME']}", 'secrets', "ansible-vault-#{m[1]}" )
      syntax_check_command = "ansible-playbook --syntax-check --vault-password-file=#{ansible_vault_password_file} playbooks/#{m[1]}/#{m[2]}.yml"
    else
      syntax_check_command = "ansible-playbook --syntax-check playbooks/#{m[1]}/#{m[2]}.yml"
    end
    if system( syntax_check_command )
      n "Ansible playbook syntax-check passed!", m[1], :success
    else
      n "Ansible playbook syntax-check FAILED!", m[1], :failed
    end
  end

  watch( /roles\/(.+?)\/(.*)\.yml$/ ) do |m|
    # Create temporary playbook dir structure + play that includes role
    ansible_guard_tmpdir = File.join( Dir.tmpdir, 'ansible-guard')
    ansible_guard_playbook_tmpdir = File.join( ansible_guard_tmpdir, 'playbooks', "#{m[1]}" )

    FileUtils.mkdir_p ansible_guard_tmpdir
    FileUtils.mkdir_p ansible_guard_playbook_tmpdir
    FileUtils.mkdir_p File.join( ansible_guard_tmpdir, 'inventory' )
    File.open( File.join( ansible_guard_tmpdir, 'inventory', 'hosts'), 'w') do |hosts_file|
      begin
        hosts_file.write("[local]\nlocalhost ansible_connection=local\n")
      ensure
        hosts_file.close
      end
    end

    File.symlink( File.join(Dir.pwd, 'roles'), File.join( ansible_guard_tmpdir, 'roles' ) )
    File.symlink( File.join(Dir.pwd, 'roles'), File.join( ansible_guard_playbook_tmpdir, 'roles' ) )

    begin
      Tempfile.create("#{m[1]}.yml", ansible_guard_playbook_tmpdir) do |file|
        
        File.open(file, 'w') do |test_playbook|
          file.write <<-EOF.gsub(/^ {12}/, '')
            # Temporary playbook file to include the role to syntax-check
            ---
            - name: wrapper playbook for testing "#{m[1]}"
              hosts: localhost
              roles:
                - #{m[1]}
          EOF
          # file.rewind
          # puts file.read
          file.close
        end

        Dir.chdir ansible_guard_tmpdir do
          # puts Dir.pwd
          # puts Dir.glob( '*' )
          # Dir.glob( '*' ).each do |dir|
          #   puts system("ls -lR #{dir}")
          # end
          # puts "FILE CONTENTS:"
          # puts File.open(file.path, 'r').read
          # puts "ansible-playbook -i #{File.join( ansible_guard_tmpdir, 'inventory' )} --syntax-check #{file.path}"
          if system("ansible-playbook -i #{File.join( ansible_guard_tmpdir, 'inventory' )} --syntax-check #{file.path}")
            n "Ansible role syntax-check passed!", m[1], :success
          else
            n "Ansible role syntax-check FAILED!", m[1], :failed
          end
        end
      end
    ensure
       # file.close
       # file.unlink   # deletes the temp file
       FileUtils.rm_rf ansible_guard_tmpdir
    end
  end
end
