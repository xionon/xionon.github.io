require 'date'
require 'fileutils'

desc "Create a new post"
task :post do
  date = Date.today.strftime("%Y-%m-%d")
  drafts = Dir['./_drafts/*']

  if drafts.empty?
    puts "No drafts to publish"
  else
    puts "Post which draft?"

    drafts.each_with_index do |draft, idx|
      puts "#{idx} - #{draft}"
    end
    puts ""
    print "Enter a number: "
    index = STDIN.gets.chomp.to_i

    puts "Publishing #{drafts[index]}"
    filename = [date, File.basename(drafts[index])].join('-')
    FileUtils.mv("#{drafts[index]}", File.join("_posts", filename))
  end
end

desc "Create a new draft"
task :draft do
  print "Title: "
  title = STDIN.gets.chomp

  filename_title = title.gsub(/[^[[:alnum:]] ]/i, '').split(" ").map(&:downcase)
  filename = filename_title.join('-')

  File.open("_drafts/" + filename + ".markdown", "w+") do |draft|
    draft.puts(<<-DRAFT)
---
layout: post
title: "#{title}"
---
    DRAFT
  end
end
