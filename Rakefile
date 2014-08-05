require 'review'

re_files = File.read("./catalog.yml").scan(/\w*?\.re/)

rule '.re' => ['.md'] do |t|
  sh "bundle exec md2review #{t.source} > #{t.name}"
end

desc "generate pdf"
file "c86.pdf" => re_files + %w{catalog.yml config.yml locale.yml}  do |t|
  Rake::Task[:clean_pdf].invoke
  sh "bundle exec review-pdfmaker config.yml"
end

task :clean_pdf do
  sh "rm -r c86-pdf" if File.exists?("c86-pdf") && File.directory?("c86-pdf")
  sh "rm c86.pdf" if File.exists?("c86.pdf")
end

task :default => "c86.pdf"
