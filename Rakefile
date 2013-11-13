require 'rubygems'
require 'rake'
require 'rdoc'
require 'date'
require 'yaml'
require 'tmpdir'
require 'jekyll'
require 'git'

desc "Generate blog files"
task :generate do
  Jekyll::Site.new(Jekyll.configuration({
    "source"      => ".",
    "destination" => "_site"
  })).process
end


desc "Generate and publish blog to gh-pages"
task :publish => [:generate] do

  if confirm == 'y'
    Dir.mktmpdir do |tmp|
      system "cp -R _site/* #{tmp}"
      system "git checkout gh-pages"
      puts 'make sure branch checked out successfully, y to continue: '
      confirm2 = $stdin.gets.chomp
      if confirm2
        system "rm -rf *"
        system "mv #{tmp}/* ."
        message = "Site updated at #{Time.now.utc}"
        system "git add ."
        system "git commit -am #{message.shellescape}"
        system "git push origin gh-pages"
        system "git checkout master"
        system "echo yolo"
      end
    end
end

task :default => :publish