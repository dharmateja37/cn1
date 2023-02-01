# cn1
1.WriteaC/C++programtoimplementthedatalinklayerframingmethods.
A) bitstuffing
#include<stdio.h>
#include<string.h>
voidmain()
{
chardata[50],stuff[50];
inti,j,count,len;
printf("enterthedata\n");
scanf("%s"
,data);
len=strlen(data);
count=0;
j=0;
for(i=0;i<len;i++)
{
if(data[i]==
'1') count++;
else count=0;
stuff[j]=data[i];
j++;
if(count==5&&data[i+1]==
'1')
{
stuff[j]=
'0';
j++;
count=0;
}
}
printf("Stuffeddatais: \n01111110 %s 01111110"
,stuff);
getch();
}
Output
Enterthedata:
01111110110
Stuffeddatais:
01111110 011111010110 01111110
B)Characterstuffing
#include<stdio.h>
#include<string.h>
voidmain(){
charframe[50][50],str[50][50];
charflag[10];
strcpy(flag,
"flag");
charesc[10];
strcpy(esc,
"esc");
inti,j,k=0,n;
strcpy(frame[k++],
"flag");
printf("Enterno.ofString:\t");
scanf("%d"
,&n);
printf("EnterString\n");
for(i=0;i<=n;i++)
{
gets(str[i]);
}
printf("Youentered:\n");
for(i=0;i<=n;i++)
{
puts(str[i]);
}
printf("\n");
for(i=1;i<=n;i++)
{
if(strcmp(str[i],flag)!=0&&strcmp(str[i],esc)!=0)
{
strcpy(frame[k++],str[i]);
}
else
{
strcpy(frame[k++],
"esc");
strcpy(frame[k++],str[i]);
}
}
strcpy(frame[k++],
"flag");
printf("------------------------------\n");
printf("Bytestuffingat senderside:\n\n");
printf("------------------------------\n");
for(i=0;i<k;i++)
{
printf("%s\t"
,frame[i]);
}
}
2.WriteaC/C++programtoimplementDistanceVectorRouting Algorithm.
#include<stdio.h>
structrouting_table
{
intdist[10],nexthop[10];
};
structrouting_tablenetworknodes[10];
voidinit(intn)
{
inti,j;
for(i=0;i<n;i++)
{
for(j=0;j<n;j++)
{
if(i!=j) {
nodes[i].dist[j]=999;
nodes[i].nexthop[j]=-20;
}
nodes[i].dist[i]=0;
nodes[i].nexthop[i]=-20;
}
}
}
voidupdate(inti,intj,int k)
{
nodes[i].nexthop[j]=k;
nodes[i].dist[j]=nodes[i].dist[k]+nodes[k].dist[j];
}
voiddvr(intn)
{
inti,j,k;
for(i=0;i<n;i++)
for(k=0;k<n;k++)
for(j=0;j<n;j++)
if(nodes[i].dist[j]>(nodes[i].dist[k]+nodes[k].dist[j]))
{update(i,j,k); }
}
voidmain()
{
intn,i,j;
printf("enterthenumofnodes\n");
scanf("%d"
,&n);
init(n);
printf("enterthedistancesmetric\n");
for(i=0;i<n;i++)
{
printf("enterthenode%c routingtable \n"
,65+i);
for(j=0;j<n;j++)
scanf("%d"
,&nodes[i].dist[j]);
}
dvr(n);
printf("distancevectorroutingalgorithm\n");
for(i=0;i<n;i++)
{
printf("Updatednode%c table\n"
,65+i);
printf("\tDEST\tDIST\tHOP\n");
for(j=0;j<n;j++)
if(i!=j)
{
printf("\t%c\t%d \t%c\n"
,65+j,nodes[i].dist[j],65+nodes[i].nexthop[j]);
}
}
}
Output
enterthenumofnodes
5
enterthedistancesmetric
enterthenodeAroutingtable
05 2399
enterthenodeBroutingtable
50 499 3
enterthenodeCroutingtable
24 099 4
enterthenodeDroutingtable
39999099
enterthenodeEroutingtable
99 34990
distance vectorrouting algorithm
Updated nodeA table
DEST DIST HOP
B 5 -
C 2 -
D 3 -
E 6 C
Updated nodeB table
DEST DIST HOP
A 5 -
C 4 -
D 8 A
E 3 -
Updated nodeC table
DEST DIST HOP
A 2 -
B 4 -
D 5 A
E 4 -
Updated nodeD table
DEST DIST HOP
A 3 -
B 8 A
C 5 A
E 9 A
Updated nodeE table
DEST DIST HOP
A 6 C
B 3 -
C 4 -
D 9 C
3.WriteaC/C++ProgramToImplementStopandWaitFlowControlProtocol.
#include<time.h>
#include<stdio.h>
#include<stdlib.h>
#defineTIMEOUT5
#defineMAX_SEQ1
#defineTOT_PACKETS3
#defineinc(k)if(k<MAX_SEQ) k++;elsek=0;
typedefstruct
{
intdata;
}packet;
typedefstruct
{
intkind;
intseq;
intack;
packetinfo;
interr;
}frame;
frameDATA;
typedefenum{frame_arrival,err,timeout,no_event}event_type;
voidfrom_network_layer(packet*);
voidto_network_layer(packet *);
voidto_physical_layer(frame*);
voidfrom_physical_layer(frame*);
voidwait_for_event_sender(event_type*);
voidwait_for_event_reciever(event_type*);
voidreciever();
voidsender();
inti=1; //Datatobesentbysender
charturn=
's'; //r,s
intDISCONNECT=0;
/*__________________________________________________________________________*/
intmain()
{
//clrscr();
//rand();
while(!DISCONNECT)
{
sender();
for(longinti=0;i<1000000;i++); //delay(40);
reciever();
}
return0;
}
/*__________________________________________________________________________*/
voidsender()
{
staticintSn=0;
//staticframes;
staticframer,s;
packetbuffer;
event_typeevent;
staticintflag=0;
if(flag==0)
{
from_network_layer(&buffer);
s.info=buffer;
s.seq=Sn;
printf("\nSENDER: Info=%d seqno=%d "
,s.info,s.seq);
inc(Sn);
turn=
'r';
to_physical_layer(&s);
flag=1;
}
wait_for_event_sender(&event);
if(turn==
's')
{
if(event==frame_arrival) //ackrecieved
{ from_physical_layer(&r);
if(r.seq==Sn)
flag=0;
}
if(event==timeout)
{
printf("\nSENDER:ResendingFrame ");
turn=
'r';
to_physical_layer(&s);
}
}
}
/*__________________________________________________________________________*/
voidreciever()
{
staticintRn=0;
staticframefr,fs;
event_typeevent;
wait_for_event_reciever(&event);
if(turn==
'r')
{
if(event==frame_arrival)
{
from_physical_layer(&fr);
if(fr.seq==Rn)
{inc(Rn);
to_network_layer(&fr.info);
printf(" \n\tACKSENT%d"
,Rn);
}
else
printf("\nRECIEVER:DuplicateFrame....AcknowledgementResent\n");
turn=
's';
fs.seq=Rn;
to_physical_layer(&fs);
}
if(event==err)
{
printf("\nRECIEVER:CorruptedFrame\n");
turn=
's'; //ifframenotrecieved
} //sendersholdsenditagain
}// ifturn
}//voidreceiver
/*__________________________________________________________________________*/
voidfrom_network_layer(packet*buffer)
{
(*buffer).data=i;
i++;
}
/*___________________________________________________________________________*/
voidto_physical_layer(frame*s)
{ staticintcount=1; //0meanserror
s->err=rand()%2; //nonzeromeansnoerror
printf("\n\terrorrate=%d"
,s->err);
DATA=*s; //probabilityoferror=1/4
}
/*___________________________________________________________________________*/
voidto_network_layer(packet *buffer)
{
printf("\nRECIEVER:Packet%drecieved \n"
,(*buffer).data);
if(i>TOT_PACKETS) //ifallpacketsrecievedthendisconnect
{
DISCONNECT=1;
printf("\nDISCONNECTED");
}
}
/*___________________________________________________________________________*/
voidfrom_physical_layer(frame*buffer)
{
*buffer=DATA;
}
/*___________________________________________________________________________*/
voidwait_for_event_sender(event_type*e)
{
staticinttimer=0;
if(turn==
's')
{
timer++;
if(timer==TIMEOUT)
{
*e=timeout;
printf("\nSENDER:Acknotrecieved=>TIMEOUT\n");
timer=0;
return;
}
if(DATA.err==0) *e=err;
else
{ timer=0; *e=frame_arrival; //ack
}
}
}
/*____________________________________________________________________________*/
voidwait_for_event_reciever(event_type*e)
{
if(turn==
'r')
{
if(DATA.err==0)
*e=err;
else
*e=frame_arrival;
}
}
SampleOutput1:
SENDER : Info=1 seqNo=0
errorrate=1 RECIEVER:Packet1recieved,AckSent
errorrate=1 SENDER: Info=2 seqno=1
errorrate=0 RECIEVER:CorruptedFrame
SENDER:Acknotrecieved=>TIMEOUT
SENDER:ResendingFrame
errorrate=1 RECIEVER:Packet2recieved,AckSent
errorrate=1 SENDER: Info=3 seqno=0 errorrate=1
RECIEVER:Packet3recieved,AckSent
DISCONNECTED
SampleOutput2
SENDER: Info=1 seqno=0
errorrate=1
RECIEVER:Packet1recieved
ACKSENT1
errorrate=2
SENDER: Info=2 seqno=1
errorrate=3
RECIEVER:Packet2recieved
ACKSENT0
errorrate=0
SENDER:Acknotrecieved=>TIMEOUT
SENDER : Resending Frame
error rate =1
RECIEVER : Duplicate Frame.... Acknowledgement Resent
error rate =2
SENDER : Info = 3 seq no = 0
error rate =3
RECIEVER :Packet 3 recieved
DISCONNECTED
ACK SENT 1
error rate =0
4.WriteaC/++ProgramforERRORdetectingcodeusingCRC-CCITT(16bit).
#include<stdio.h>
#include<string.h>
#include<conio.h>
#defineNstrlen(g)
chart[128],cs[128],g[]=
"10001000000100001";
inta,e,c;
voidxor(){
for(c=1;c<N;c++)cs[c]=((cs[c]==g[c])?'0':'1');
}
voidcrc(){
for(e=0;e<N;e++)cs[e]=t[e];
do{
if(cs[0]==
'1')xor();
for(c=0;c<N-1;c++)cs[c]=cs[c+1];
cs[c]=t[e++];
}while(e<=a+N-1);
}
intmain(){
//clrscr();
printf("\nEnterpoly:");scanf("%s"
,t);
printf("\nGeneratingPolynomialis:%s"
,g);
a=strlen(t);
for(e=a;e<a+N-1;e++)t[e]=
'0';
printf("\nModifiedt[u]is:%s"
,t);
crc();
printf("\nChecksumis:%s"
,cs);
for(e=a;e<a+N-1;e++)t[e]=cs[e-a];
printf("\nFinalCodewordis:%s"
,t);
printf("\nTestErrordetection0(yes)1(no)?:");
scanf("%d"
,&e);
if(e==0){
printf("Enterpositionwhereerroristoinserted:");
scanf("%d"
,&e);
t[e]=(t[e]==
'0')?'1':'0';
printf("Errorneousdata:%s\n"
,t);
}
crc();
for(e=0;(e<N-1)&&(cs[e]!=
'1');e++);
if(e<N-1)printf("Errordetected.");
elseprintf("NoErrorDetected.");
//getch();
return0;
}
ExampleOutput:
Enterpoly:1011
GeneratingPolynomialis:10001000000100001
Modifiedt[u]is: 10110000000000000000
Checksumis: 1011000101101011
FinalCodewordis:10111011000101101011
TestErrordetection0(yes)1(no)?:0
Enterpositionwhereerroristoinserted:3
Errorneousdata:10101011000101101011
Errordetected.
5.WriteaC/C++ ProgramforCongestioncontrolusingLeakyBucketAlgorithm.
#include<stdio.h>
#include<stdlib.h>
structpacket
{
inttime;
intsize;
}p[50];
intmain()
{
inti,n,m,k=0;
intbsize,bfilled,outrate;
printf("Enterthenumberofpackets:");
scanf("%d"
,&n);
printf("Enterpacketsintheorderoftheyarearrivaltime\n");
for(i=0;i<n;i++)
{
printf("Enterthetimeandsize:");
scanf("%d%d"
,&p[i].time,&p[i].size);
}
printf("Enterthebucketsize:");
scanf("%d"
,&bsize);
printf("Entertheoutputrate:");
scanf("%d"
,&outrate);
m=p[n-1].time;
i=1;
k=0;
bfilled=0;
while(i<=m||bfilled!=0)
{
printf("\n\nAttime%d"
,i);
if(p[k].time==i)
{
if(bsize>=bfilled+p[k].size)
{
bfilled=bfilled+p[k].size;
printf("\n%dbytepacketisinserted"
,p[k].size);
k=k+1;
}
else
{
printf("\n%dbytepacketisdiscarded"
,p[k].size);
k=k+1;
}
}
if(bfilled==0)
{
printf("\nNopacketstotransmitte");
}
elseif(bfilled>=outrate)
{
bfilled=bfilled-outrate;
printf("\n%dbytestransfered"
,outrate);
}
else
{
printf("\n%dbytestransfered"
,bfilled);
bfilled=0;
}
printf("\nPacketsinthebucket%dbyte"
,bfilled);
i++;
}
return0;
}
ExampleOutput1:
Enterthenumberofpackets:3
Enterpacketsintheorderoftheyarearrivaltime
Enterthetimeandsize:1100
Enterthetimeandsize:2400
Enterthetimeandsize:3600
Enterthebucketsize:500
Entertheoutputrate: 200
Attime1
100bytepacketisinserted
100bytestransfered
Packetsinthebucket0byte
Attime2
400bytepacketisinserted
200bytestransfered
Packetsinthebucket200byte
Attime3
600bytepacketisdiscarded
200bytestransfered
Packetsinthebucket0byte
ExampleOutput2
Enterthetimeandsize:1100
Enterthetimeandsize:3200
Enterthetimeandsize:2400
Enterthetimeandsize:4600
Enterthebucketsize:200
Entertheoutputrate:100
Attime1
100bytepacketisinserted
100bytestransfered
Packetsinthebucket0byte
Attime2
Nopacketstotransmitted
Packetsinthebucket0byte
Attime3
200bytepacketisinserted
100bytestransfered
Packetsinthebucket100byte
Attime4
100bytestransfered
Packetsinthebucket0byt
