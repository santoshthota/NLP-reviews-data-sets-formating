#Program to output json from unstructured review dataset
require 'json'
file = File.open("Nokia6610.txt", "r")
reviews = Array.new
sentences = Array.new
features = Array.new
review = Hash.new
sentence = Hash.new
feature = Hash.new
review_count = 0
sentence_count = 0
feature_count = 0
file.each do |line|
    title_matched = /^\[t\](?<title>.*)/.match(line)
   if title_matched
      #puts "-------------------------------------------\n"
      #puts title_matched['title']
      unless sentences.empty?
          review['sentences'] = sentences 
          reviews << review
          review = {}
          sentences = []
      end
      review_count+=1
      review['id'] = review_count
      review['title'] = title_matched['title'].strip || title_matched['title']
      sentence_count = 0
      #puts review
      next
   end
   
   next if line.strip.length==0

   sentence_count+=1 #since per line only one sentance
   while true
       sentence_matched = /^\#\#(?<text>.*)/.match(line)
       if sentence_matched
          sentence['id'] = review_count.to_s+'_'+sentence_count.to_s
          sentence['text'] = sentence_matched['text'].strip || sentence_matched['text']
          sentence['features'] = features 
          sentences << sentence
          #puts sentence
          sentence = {}
          features = []
          feature_count = 0
          break
       end
       feature_matched = /(?<feature>.*?)(\[(?<opinion>\+?\-?\d)\])(?<u>(\[u\])?)(?<p>(\[p\])?)(?<rest>.*)/.match(line)
       if  feature_matched
           feature_count+=1
           feature_len = 0 #To shrink the line feature wise
           feature['id'] = review_count.to_s+'_'+sentence_count.to_s+'_'+feature_count.to_s
           feature_name = feature_matched['feature']
           feature_len+= feature_name.length
           feature_name = feature_name.strip! || feature_name
           if feature_name[0]==','
               feature['name'] = feature_name[1..feature_name.length]
           else
               feature['name'] = feature_name
           end
           feature['opinion'] = feature_matched['opinion']
           feature_len+= 4 #eg: [+2] which is 4 chars
           feature['u'] = false
           unless feature_matched['u'].empty?
               feature['u'] = true
               feature_len+= 3
           end
           feature['p'] = false
           unless feature_matched['p'].empty?
               feature['p'] = true
               feature_len+= 3
           end
           features << feature
           feature = {}
           line = line[feature_len..line.length]
       end
   end
end
unless sentences.empty?
  review['sentences'] = sentences 
  reviews << review
end
output_hash = Hash.new
output_hash['reviews'] = reviews
#puts output_hash.to_json
puts 'writing output to json file...'
File.open('/home/santosh/code/json_output.json', 'w') { |file| file.write(output_hash.to_json.to_s) }
puts 'Written'
