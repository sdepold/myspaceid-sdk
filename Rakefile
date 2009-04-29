require 'rake/testtask'
require 'rake/packagetask'
# require 'rake/rdoctask'
require 'hoe'

$LOAD_PATH.push('lib')
require 'myspace.rb'

Hoe.new('myspaceid-sdk', MySpace::VERSION) do |p|
  p.author = 'Christopher B. Baker'
  p.email = 'cbaker@myspace.com'
  p.rubyforge_name = 'myspaceid-sdk'
  p.extra_deps = ['ruby-openid', 'oauth', 'json']
end

desc "Generate manifest file programmatically"
task :generate_manifest do
  files = FileList[
                   'README.txt', 'lib/**/*', 'test/**/*', 'samples/**/*'
                  ].exclude(/db\/cstore|log\/|public\/doc|tmp/)
  
  File.rename('Manifest.txt', "Manifest-#{Time.now.to_i.to_s}.txt") if File.exists?('Manifest.txt')
  File.open('Manifest.txt', 'w') do |f|
    files.each do |name|
      f.write(name + "\n")
    end
  end
end

# desc "Build the rubygem for the SDK"
# task 'build-gem' => [] do
#   sh %{gem build myspaceid-sdk.gemspec}
# end

# desc "Build the online documetation for the SDK"
# task 'build-docs' => [] do
#   sh %{rdoc --fmt html}
# end

desc "Run the unit tests"
Rake::TestTask.new do |t|
  t.libs << "test"
  t.test_files = 'ts_alltests.rb'
  t.verbose = true
end
# Rake::RDocTask.new('rdoc') do |t|
#   t.rdoc_files.include('README', 'lib/**/*.rb')
#   t.main = 'README'
#   t.title = "MySpaceID SDK documentation"
# end

# rubyforge_project = 'myspaceid-sdk'
# rubyforge_user = 'cbaker'
# rubyforge_path = "/var/www/gforge-projects/#{rubyforge_project}/"
# desc 'Upload documentation to RubyForge.'
# task 'upload-docs' => ['rdoc'] do
#   sh "scp -r html/* " + "#{rubyforge_user}@rubyforge.org:#{rubyforge_path}"
# end

desc "Generate doc files, but deal with source control as well"
task 'generate-docs' do
  sh %{git rm -rf doc}
  sh %{rake docs}
  sh %{git add doc}
  sh %{git commmit -m 'autogenerated docs' doc}
end
