lemmatizer
==========

Lemmatizer for text in English.  Inspired by Python's [nltk.corpus.reader.wordnet.morphy](orpusReader.morphy) package.

Based on code posted by mtbr at his blog entry [WordNet-based lemmatizer](http://d.hatena.ne.jp/mtbr/20090303/prfrnlprubyWordNetbasedlemmatizer)

Forked by David Mountain, to return nil for the lemma function, if a word is not included in the dictionary


Installation
------------

    sudo gem install lemmatizer
    

Usage
-----

    require "lemmatizer"
    
    lem = Lemmatizer.new
    
    p lem.lemma("dogs",    :noun ) # => "dog"
    p lem.lemma("hired",   :verb ) # => "hire"
    p lem.lemma("hotter",  :adj  ) # => "hot"
    p lem.lemma("better",  :adv  ) # => "well"
	
	# when part-of-speech symbol is not specified as the second argument, 
	# lemmatizer tries :verb, :noun, :adj, and :adv one by one in this order.
	p lem.lemma("fired")           # => "fire"
	p lem.lemma("slow")            # => "slow"

Limitations
-----------
    
	 # This fork returns a lemma (looked up in dictionary) if there
	 # was a match with a our dictionary terms (e.g. walk, walking)
	 # but nil if there was no match (e.g twerk, twerking)
	 # Allows alt action to be taken if no lemma found
    
	# If an inflected form is included as a lemma in the word index,
	# lemmatizer may not give an expected result.
    p lem.lemma("higher", :adj) # => "higher" not "high"!
	
	# The above has to happen because "higher" is itself an entry word listed in dict/index.adj .
	# Modify dict/index.{noun|verb|adj|adv} if necessary.