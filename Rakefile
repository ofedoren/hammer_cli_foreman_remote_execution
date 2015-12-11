require 'bundler/gem_tasks'
require 'rake/testtask'
require 'ci/reporter/rake/minitest'

Rake::TestTask.new :test do |t|
  t.libs.push "lib"
  t.test_files = Dir.glob('test/**/*_test.rb')
  t.verbose = true
end

namespace :gettext do
  desc 'Update pot file'
  task :find do
    require 'hammer_cli_foreman_remote_execution/version'
    require 'hammer_cli_foreman_remote_execution/i18n'
    require 'gettext/tools'

    domain = HammerCLIForemanRemoteExecution::I18n::LocaleDomain.new
    GetText.update_pofiles(domain.domain_name, domain.translated_files,
                           "#{domain.domain_name} #{HammerCLIForemanRemoteExecution.version}",
                           :po_root => domain.locale_dir)
  end
end

namespace :pkg do
  desc 'Generate package source gem'
  task :generate_source => :build
end

task :default => :test
