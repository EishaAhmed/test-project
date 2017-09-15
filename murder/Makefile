all:
	@echo "Starting murder makefile"
	@touch README.txt
	@curl -O https://raw.githubusercontent.com/fivethirtyeight/data/master/murder_2016/murder_2015_final.csv
	@head -n1 murder_2015_final.csv >> murder_header.csv
	@tail -n+2 murder_2015_final.csv | sort >> murder_data.csv
	@awk 'BEGIN{FS=",";} $$2=="Illinois"' murder_data.csv >> murder_illinois.csv
	@awk 'BEGIN{FS=",";} $$2=="Maryland"' murder_data.csv | wc -l >> murder_maryland.count
	@awk 'BEGIN{FS=",";} {print $$3 "," $$4}' murder_illinois.csv >> murder_illinois_2014-2015.csv
	@echo "Murder processing complete"


