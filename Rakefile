require 'bundler/gem_tasks'
require 'bundler/setup'
require 'pry'

task :submodule do
  sh 'git submodule update --init' unless File.exist?('SlickGrid/MIT-LICENSE.txt')
end

task :pry do
  binding.pry
end

def move_slick(glob, target)
  Dir.glob(glob).each do |f|
    prefix = File.dirname(f).gsub(/SlickGrid\/?/,'')
    prefix = "/#{prefix}" if prefix.length > 0
    total_target = "#{target}#{prefix}"
    mkdir_p total_target unless Dir.exists? total_target
    basename = File.basename(f)
    cp f, "#{total_target}/#{basename}"
  end

end

desc "Remove the vendor directory"
task :clean do
  rm_rf 'vendor'
end

task :update_slickgrid => :submodule do
  target_dir = "vendor/assets"
  move_slick('SlickGrid/{controls/,plugins/,}*.js', "#{target_dir}/javascripts/slickgrid" )
  move_slick('SlickGrid/{controls/,plugins/,}*.css', "#{target_dir}/stylesheets/slickgrid" )
  move_slick('SlickGrid/images/*.{png,gif}', "#{target_dir}/images/slickgrid" )
end
