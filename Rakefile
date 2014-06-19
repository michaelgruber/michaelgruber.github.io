INPUT = "#{ File.dirname(__FILE__) }/_assets/sass/manifest.scss"
OUTPUT = "#{ File.dirname(__FILE__) }/css/main.css"

desc "compile sass from ./_assets/sass to ./css"
task :build do
  compile_sass
  system "jekyll build"
end


desc "watch all files for changes"
multitask watch: ['watch:sass', 'watch:jekyll']
namespace :watch do
  task :sass do
    system "bundle exec sass --watch #{ INPUT }:#{ OUTPUT } --style compressed"
  end

  task :jekyll do
    system "bundle exec jekyll serve --watch"
  end
end

def compile_sass
  system "bundle exec sass #{ INPUT }:#{ OUTPUT } --style compressed"
end
