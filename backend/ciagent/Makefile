ifeq ($(shell uname -p|sed -e 's/amd64/x86_64/g'), x86_64)
LDPATH=\
	-L. \
	-L../util/\
        -L../log/\
        -L../pool/\
        -L../net/\
        -L../threadpool/linux/\
	-L../libs/64/\
	-L/usr/lib64\
	-L/home/a/lib64\

STATLIB= ../log/liblog.a ../net/libnet.a ../poll/libepollmanager.a  ../threadpool/linux/libthreadpool.a ../config/libconfig.a ../thread/libsmartthread.a ../sync/libsync.a ../pty/libpopen.a ../daemon/libdaemon.a ../libs/64/liblog4cpp.a ../libs/64/libcurl.a ../libs/64/libjson.a


else
LDPATH=\
	-L. \
	-L../util/\
        -L../log/\
        -L../pool/\
        -L../net/\
        -L../threadpool/linux/\
	-L../libs/32/\
	-L/usr/lib/\
	-L/home/a/lib\

STATLIB= ../log/liblog.a ../net/libnet.a ../poll/libepollmanager.a  ../threadpool/linux/libthreadpool.a ../config/libconfig.a ../thread/libsmartthread.a ../sync/libsync.a ../pty/libpopen.a ../daemon/libdaemon.a ../libs/32/liblog4cpp.a ../libs/32/libcurl.a ../lib/32/libjson.a

endif

LINK= -lpthread -ldl -lrt -lapr-1 -lsvn_subr-1 -lsvn_fs-1 -lsvn_client-1

INCLUDE=\
	-I. \
        -I../include/log4cpp\
        -I../include\
        -I../util/thread\
        -I../util\
        -I../net\
        -I../poll\
        -I../threadpool\
        -I../log\
        -I/usr/include/subversion-1\
        -I/usr/include/apr-1

CC = gcc
GCC = g++ -g

ifeq ($(coverage), yes)
CFLAG = -g -Wall $(INCLUDE) -fprofile-arcs -ftest-coverage
else
CFLAG = -g -Wall $(INCLUDE)
endif


all: toast

toast: AgentEngine.o AgentThread.o agentconnection.o agentinformation.o linuxgetsystemperfinfo.o citaskmanager.o AgentMain.cpp 
	$(GCC) $(LDPATH) ${CFLAG} -o $@ AgentThread.o AgentEngine.o agentconnection.o agentinformation.o linuxgetsystemperfinfo.o citaskmanager.o AgentMain.cpp ${LINK} $(STATLIB)

AgentEngine.o: AgentEngine.cpp $(STATLIB)
	$(GCC) -c $(LDPATH) $(CFLAG) -o $@ AgentEngine.cpp
agentconnection.o: agentconnection.cpp $(STATLIB)
	$(GCC) -c $(LDPATH) $(CFLAG) -o $@ agentconnection.cpp
AgentThread.o: AgentThread.cpp $(STATLIB)
	$(GCC) -c $(LDPATH) $(CFLAG) -o $@ AgentThread.cpp
agentinformation.o: agentinformation.cpp $(STATLIB)
	$(GCC) -c $(LDPATH) $(CFLAG) -o $@ agentinformation.cpp
linuxgetsystemperfinfo.o: linuxgetsystemperfinfo.cpp $(STATLIB)
	$(GCC) -c $(LDPATH) $(CFLAG) -o $@ linuxgetsystemperfinfo.cpp	
citaskmanager.o: citaskmanager.cpp $(STATLIB)
	$(GCC) -c $(LDPATH) $(CFLAG) -o $@ citaskmanager.cpp

clean:
	rm -f *.o
	rm -f *.gcno
	rm -f *.gcda
	rm -f toastagent
