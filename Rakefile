require "rubygems"
require "bundler/setup"
require "stringex"

current_dir = File.expand_path(File.dirname(__FILE__))

# usage rake new_app[app_name]
desc "Creates a new manifest file to deploy the blog to cloud foundry"
task :new_app, :name do |t, args|
  raise "### You need to provide an application name" unless !args.name.nil?
  appname = args.name
  filename = "manifest.yml"
  if File.exist?(filename)
    abort("rake aborted!") if ask("#{filename} already exists. Do you want to overwrite?", ['y', 'n']) == 'n'
  end
  puts "Writing manifest file: #{filename}"

  manifest = IO.read("#{current_dir}/manifest.yml")
  dest_manifest = "#{current_dir}/../manifest.yml"

  File.open(dest_manifest, 'w') do |f|
    f.write manifest.sub!("app_name", appname)
  end

  puts "Copying static node.js server"
  FileUtils.cp("#{current_dir}/app.js", "#{current_dir}/../app.js")

  puts "Copying .vmcignore file"
  FileUtils.cp("#{current_dir}/vmcignore", "#{current_dir}/../.vmcignore")

  puts "Copying npm-shrinkwrap file"
  FileUtils.cp("#{current_dir}/npm-shrinkwrap.json", "#{current_dir}/../npm-shrinkwrap.json")

  puts "Copying cloudfoundry.json"
  FileUtils.cp("#{current_dir}/cloudfoundry.json", "#{current_dir}/../cloudfoundry.json")

end

## From octopress Rakefile
## maybe we can include these somehow without the need for copy paste.
def get_stdin(message)
  print message
  STDIN.gets.chomp
end

def ask(message, valid_options)
  if valid_options
    answer = get_stdin("#{message} #{valid_options.to_s.gsub(/"/, '').gsub(/, /,'/')} ") while !valid_options.include?(answer)
  else
    answer = get_stdin(message)
  end
  answer
end
