desc 'generate pdf'
task :generate do
  require 'kramdown'
	require 'pdfkit'
	header = File.read('./header.html')
  footer = "</body></html>"
	body = Kramdown::Document.new(File.read('./doc/test.md')).to_html

	File.open('./temp.html', 'w') do |f|
    [header, body, footer].each {|s| f.puts s}
  end
end

desc 'generate pdf'
task :pdf do
	html = File.read('./temp.html')
	kit = PDFKit.new(html, :page_size => 'A4')
	kit.to_file('./test.pdf')
end

