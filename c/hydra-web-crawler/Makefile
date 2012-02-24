CC= gcc

hwc: main.o web.o parse.o redis-slave.o
	$(CC) -Wall -o hwc web.o main.o parse.o redis-slave.o -lcurl -Lhiredis -lhiredis

main.o: main.c
	$(CC) main.c -Wall -c

web.o: web.c web.h
	$(CC) web.c -Wall -c

parse.o: parse.c parse.h
	$(CC) parse.c -Wall -c

redis-slave.o: redis-slave.c redis-slave.h
	$(CC) redis-slave.c -Wall -c


# clean and other non compile actions:
clean:
	rm -rf hwc *.out *.o

clean~:
	rm -f *~

cleanout:
	rm -f dirout/*

makerun: hwc
	./hwc

deps:
#	removed redis.. since we can use ubuntu built in
#	@cd redis-2.2.12 && make
	@cd hiredis && make && make install
	/sbin/ldconfig
	@cd tests/cu && make
	@cd tests && make

startdb:
	redis-2.2.12/src/redis-server redis-2.2.12/redis.conf
