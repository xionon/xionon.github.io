require 'date'
require 'fileutils'

desc "Create a new post"
task :post do
  print "Title: "
  title = STDIN.gets.chomp

  date = Date.today
  filename_title = title.gsub(/[^[[:alnum:]] ]/i, '').split(" ").map(&:downcase)
  filename = ([date.year, date.month, date.day] + filename_title).join('-')

  File.open("_posts/" + filename + ".markdown", "w+") do |post|
    post.puts(<<-POST)
---
layout: post
title: "#{title}"
---
    POST
  end
end
