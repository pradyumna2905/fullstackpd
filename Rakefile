desc 'Create a new post with provided name'
task :new do
  require './lib/post_creator.rb'
  toplevel_directory = Rake.application.find_rakefile_location[1]
  PostCreator.new(toplevel_directory).create
end
