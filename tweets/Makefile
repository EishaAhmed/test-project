download:
	@mkdir data
	@curl www.derekruths.com/static/reading_tweets/books_tweets100000.txt.gz >> ./data/books_tweets100000.txt.gz
prep:
	@echo "Unzipping file..."
#	@gunzip ./data/books_tweets100000.txt.gz
	@echo "Converting JSON tweet data to TSV..."
	@cat ./data/books_tweets100000.txt | jq -r "[.user.id, .created_at, .user.lang, .text] | @tsv" > ./data/book_tweets.tsv
	@echo "Creating tweet subsets..."
	@awk 'BEGIN{ FS="\t" } $$2 ~ /Oct 23/ ' ./data/book_tweets.tsv > ./data/tweetsOct2012.tsv
	@awk 'BEGIN{ FS="\t" } $$4 ~ /\#gameofthrones/ ' ./data/book_tweets.tsv > ./data/tweets_got.tsv
	@echo "Prep complete!"
analyze:
	@echo "Number of Russian tweets: " > results.txt
	@awk 'BEGIN{ FS="\t" } $$3 ~ /^ru/ ' ./data/book_tweets.tsv | wc -l >> results.txt
	@echo "Number of tweets from August 2016: " >> results.txt
	@awk 'BEGIN{ FS="\t" } $$2 ~ /Aug(.*)2016/ ' ./data/book_tweets.tsv | wc -l >> results.txt
	@echo "Number of tweets that contain a retweet: " >> results.txt
	@awk 'BEGIN{ FS="\t" } $$4 ~ /^RT/ ' ./data/book_tweets.tsv | wc -l >> results.txt
	@echo "Number of tweets that mention #gameofthrones: " >> results.txt
	@awk 'BEGIN{ FS="\t" } $$4 ~ /\#gameofthrones/ ' ./data/book_tweets.tsv | wc -l >> results.txt

