# frozen_string_literal: true

require "bundler/gem_tasks"
require "rubocop/rake_task"
require "rake/testtask"

RuboCop::RakeTask.new

Rake::TestTask.new do |t|
  t.test_files = FileList["test/anycable/test_*.rb",
    "test/anycable/**/test_*.rb"]
end

namespace :anyt do
  task :rack do
    Dir.chdir(File.join(__dir__, "test/support/rack")) do
      sh 'anyt -c "puma config.ru" --except features/server_restart'
    end
  end

  task :rails do
    Dir.chdir(File.join(__dir__, "test/support/rails")) do
      sh 'anyt -c "puma config.ru" --skip-rpc --wait-command=5 -r ./anyt.rb --except features/server_restart'
    end
  end
end

task anyt: ["anyt:rack", "anyt:rails"]

task default: [:rubocop, :test, :anyt]
