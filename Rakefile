require 'fileutils'
require 'tempfile'
require 'pathname'

desc 'Install Universal Test Runner'
task 'install' do
  source = Pathname(__FILE__) + '../bin/rut'
  dest   = Pathname("/usr/local/bin/#{source.basename}")
                    
  # Hard-code the shebang
  Tempfile.open("install-#{source.basename}") do |output|
    open(source, 'r') do |input|
      input.gets                # drop original shebang
      output.puts "#!#{RUBY}"   # hardcode system-specific shebang
      while chunk = input.read(1024)
        output.write(chunk) 
      end
    end
    output.close
    install output.path, dest, :mode => 0755, :verbose => true
  end
end
