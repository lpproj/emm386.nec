#
# to compile and build, you need TASM and TC 2.01
#
# building with TCPP 1.0 should be possible, but requires 
# a different LIBM.LIB (this one was taken from FreeDOS kernel)
# and hasn't been tried
#
# if you use different compiler/assembler/linker
# please don't complain
#

TCC=$(TCBASE)\tcc -G- -w -r -N- -O -Z -k- -g1

all: ..\emm386.exe emmtest.exe ..\himem.exe ..\himemsm.exe


..\emm386.exe: emm386.exe
	$(SY2PACK) emm386.exe
	copy emm386.exe ..

..\himem.exe: himem.exe
	$(SY2PACK) himem.exe
	copy himem.exe  ..


emm386.exe: emm386.obj emm386c.obj prf.obj useful.obj
	$(TCBASE)\tlink /3 /m emm386 emm386c prf useful libm.lib

emm386.obj: emm386.asm
	tasm /la /m3 /z /n $*.asm;

emm386c.obj: emm386c.c
	$(TCC) -c emm386c.c
	
prf.obj: prf.c
	$(TCC) -c prf.c
	
useful.obj: useful.c
	$(TCC) -c useful.c


emmtest.exe: emmtest.c
	$(TCC) -L$(TCBASE)\lib -I$(TCBASE)\include emmtest.c

himem.exe : himem.obj himemc.obj prf.obj useful.obj xmstest.obj
	$(TCBASE)\tlink /3 /m himem himemc xmstest prf useful libm.lib



himem.obj: himem.asm
	$(TASM) /m3 /z /l /n himem.asm


himemC.obj: himemC.C
	$(TCC) -c -w -g1 himemC.C


xmstest.obj: xmstest.c
	$(TCC) -c -w -g1 xmstest.c


# slightly smaller (400 byte) HIMEM implementation,
# that handles only 64MB


..\himemsm.exe: himemsm.exe
	$(SY2PACK) himemsm.exe
	copy himemsm.exe  ..

himemsm.exe : himemsm.obj himemc.obj prf.obj useful.obj xmstest.obj
	$(TCBASE)\tlink /3 /m himemsm himemc xmstest prf useful libm.lib

himemsm.obj: himemsm.asm
	$(TASM) /m3 /z /l /n himemsm.asm

