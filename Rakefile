namespace :apostila do
  desc 'prepare build'
  task :prebuild do
    Dir.mkdir 'images' unless Dir.exists? 'images'
    Dir.glob("book/*/images/*").each do |image|
      FileUtils.copy(image, "images/" + File.basename(image))
    end
  end
  desc 'Faz em html'
  task :build_html do
    puts "Converting to HTML..."
    `bundle exec asciidoctor apostila/apostila.adoc`
  end
  desc 'Faz os formatos básicos'
  task :build => :prebuild do
    puts "Converting to HTML..."
    `bundle exec asciidoctor apostila/apostila.adoc`
    puts " -- HTML output at apostila.html"
    puts "Converting to EPub..."
    `bundle exec asciidoctor-epub3 apostila/apostila.adoc`
    puts " -- Epub output at apostila.epub"
    puts "Converting to Mobi (kf8)..."
    `bundle exec asciidoctor-epub3 -a ebook-format=kf8 apostila/apostila.adoc`
    puts " -- Mobi output at apostila.mobi"
    puts "Converting to PDF... (this one takes a while)"
    `bundle exec asciidoctor-pdf apostila/apostila.adoc 2>/dev/null`
    puts " -- PDF output at apostila.pdf"
  end
end
task :default => "apostila:build"
