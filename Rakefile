require "bundler"
Bundler::GemHelper.install_tasks
require "rspec/core/rake_task"

RSpec::Core::RakeTask.new(:spec)

task :default => [:compile, :spec]
require "rake/extensiontask"

task :build => :compile
task :spec => :compile

spec = eval File.read("strptime.gemspec")
Rake::ExtensionTask.new("strptime", spec) do |ext|
  ext.ext_dir = 'ext/strptime'
  ext.cross_compile = true
  ext.lib_dir = File.join(*['lib', 'strptime', ENV['FAT_DIR']].compact)
  # cross_platform names are of MRI's platform name
  ext.cross_platform = ['x86-mingw32', 'x64-mingw32']
end

namespace :build do
  desc 'Build gems for Windows per rake-compiler-dock'
  task :windows do
    require 'rake_compiler_dock'
    RakeCompilerDock.sh 'bundle && rake cross native gem RUBY_CC_VERSION=2.0.0:2.1.7:2.2.3'
  end
end
