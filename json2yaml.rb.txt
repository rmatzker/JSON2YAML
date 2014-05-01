#!/usr/bin/env ruby

# json2yaml.rb - converts json to yaml
#
# Date  : 2/17/2013
# Author: Rob Matzker
#
# Usage: json2yaml inputfile outputfile
#
# NOTE: this requires the json gem

require 'rubygems'
require 'json'
require 'yaml'

# Check for input filename
unless ARGV.length == 2
  puts "Usage: #{$0} inputfile outputfile"
  exit
end

# Store filenames
infile = ARGV[0]
outfile = ARGV[1]

# Check if infile exists
if ! File.exists?(infile)
  puts "Input file not found: #{infile}"
  exit
end

# Parse contents of infile. If error is found, it will exit with debug info
contents = JSON.parse(File.read(infile))

# Write YAML version to outfile
File.open(outfile, 'w') { |file| file.write(contents.to_yaml) }

# Confirm we are done
puts "Converted #{infile} to #{outfile}"
