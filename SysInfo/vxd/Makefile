#****************************************************************************
#
#PCI BIOS, Memory , Interrupt handle VxD
#                                         for windows 95/98
#                                       ver 1.0 Aug 20 1999
#                                        kashiwano masahiro
#
#****************************************************************************

#
# ����VxD���R���p�C������ɂ�DDK���C���X�g�[������Ă���K�v������܂��B
# 
# 95/98�ǂ���ł�����VxD�ɂ��邽�߂ɂ�95�p��DDK���K�v�ł��B
# 98�pDDK���g�p�����ꍇ�A95�ł͓��삵�܂���B
# 95�pDDK�ł́AVC ver2.0�ɕt����LINK���g�p����K�v������܂��B

# ���ɍ��킹��PATH�͏C���K�v
RC16 = c:\mstools\binw16\rc
ML = c:\ddk\masm\ml
CL = cl
LINK = c:\ddk\vc2link\link

CFLAGS  = -Zdp -Gs -c -DIS_32 -DDEBLEVEL=1 -DDEBUG
LFLAGS     = -machine:i386 -debug:none kernel32.lib 
AFLAGS     = -coff -DBLD_COFF -DIS_32 -W2 -Zd -c -Cx -DMASM6

all: direxist bin\pcidbg95.vxd

direxist:
        if not exist bin\nul    md bin

bin\pcidbg95.res: pcidbg95.rc
       $(RC16)  -Fo$@ -r pcidbg95.rc

bin\pcidbg95.obj: pcidbg95.c
        $(CL) $(CFLAGS) -Fo$@ %s

bin\ctrl.obj: ctrl.asm
        $(ML) $(AFLAGS) -Fo$@ %s

bin\pcidbg95.vxd: bin\pcidbg95.obj bin\ctrl.obj bin\pcidbg95.res\
                  pcidbg95.def
        echo >NUL @<<pcidbg95.crf
-MACHINE:i386 -DEBUG:NONE -PDB:NONE 
-DEF:pcidbg95.def -OUT:bin\pcidbg95.vxd -MAP:bin\pcidbg95.map
-VXD vxdwraps.clb bin\pcidbg95.obj bin\ctrl.obj 
<<
        $(LINK) @pcidbg95.crf
        cd bin
        mapsym pcidbg95
	adrc2vxd pcidbg95.vxd pcidbg95.res
        cd ..

clean:
        del bin\*.obj
        del bin\*.vxd
        del bin\*.exe
        del bin\*.exp
        del bin\*.map
        del bin\*.sym
        del bin\*.lib
        del bin\*.res
        rd  bin
        del *.pdb
        