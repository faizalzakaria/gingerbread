require "rubygems"
require "tmpdir"

require "bundler/setup"
require "jekyll"

# S3 bucket
S3_BUCKET="s3://<YOUR BUCKET>"

namespace :site do
  desc "Generate blog files"
  task :generate do
    FileUtils.rm '_site', force: true
    Jekyll::Site.new(Jekyll.configuration({
      "source"      => ".",
      "destination" => "_site"
    })).process
  end

  desc "Generate and publish blog to s3"
  task :publish => [:generate] do
    puts `aws s3 sync _site #{S3_BUCKET}`
  end
end

