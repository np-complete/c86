require 'review'
require 'rake/clean'

SRCS = FileList['*.md']
OBJS = SRCS.ext('re')
PROJECT = 'c86'
PDF = "#{PROJECT}.pdf"

CLEAN.include(OBJS)
CLOBBER.include(PDF)

rule '.re' => '.md' do |t|
  sh "bundle exec md2review --render-link-as-footnote #{t.source} > #{t.name}"
end

desc "generate pdf"
file PDF => OBJS + %w{catalog.yml config.yml locale.yml}  do |t|
  rm_rf "#{PROJECT}-pdf" if File.exist?("#{PROJECT}-pdf")
  rm PDF if File.exist?(PDF)
  sh "bundle exec review-pdfmaker config.yml"
end

task :default => PDF
