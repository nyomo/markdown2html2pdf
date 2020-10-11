markdown_files = Dir.open("./docs",&:to_a).reject{ |f| f.match(%r{^\.}) }.map{|f| f.sub(/\.md/,'')}

desc 'generate pdf'
markdown_files.each do |filename|
  file "./pdf/" + filename + ".pdf" => [ "./docs/"+filename+'.md' , "./header.html" ] do
    require 'kramdown'
    header = File.read('./header.html')
    footer = "</body></html>"
    body = Kramdown::Document.new(File.read('./docs/' + filename + '.md')).to_html
    File.open('./temp.html', 'w') do |f|
      [header, body, footer].each {|s| f.puts s}
		end

    require 'pdfkit'
    html = File.read('./temp.html')
    kit = PDFKit.new(html, :page_size => 'A4')
    kit.to_file('./pdf/'+filename+'.pdf')
  end
end  

task :all => markdown_files.map { |filename| './pdf/' +filename + '.pdf' } 
