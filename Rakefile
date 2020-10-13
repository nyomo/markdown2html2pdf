markdown_files = Dir.open("./docs",&:to_a).reject{ |f| f.match(%r{^\.}) }.map{|f| f.sub(/\.md/,'')}

TXTDIR = './docs'
PDFDIR = './pdf'

desc 'generate pdf'
markdown_files.each do |filename|
  file PDFDIR+"/" + filename + ".pdf" => [ TXTDIR + "/"+filename+'.md' , "./header.html" ] do
    require 'kramdown'
    header = File.read('./header.html').gsub("BASEDIRISHERE","file://" + Dir.pwd + '/' + TXTDIR + "/")
    footer = "</body></html>"
    body = Kramdown::Document.new(File.read( TXTDIR + '/' + filename + '.md')).to_html
    File.open(TXTDIR+'/temp.html', 'w') do |f|
      [header, body, footer].each {|s| f.puts s}
                end

    require 'pdfkit'
    html = File.read(TXTDIR + '/temp.html')
    kit = PDFKit.new(html, :page_size => 'A4',:enable_local_file_access =>'true')
    kit.to_file(PDFDIR + '/'+filename+'.pdf')
  end
end

task :all => markdown_files.map { |filename| PDFDIR + '/' +filename + '.pdf' }
