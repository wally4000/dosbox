./autogen.sh && CXXFLAGS="-I${PSPDEV}/psp/sdk/include -I${PSPDEV}/psp/include/SDL -I${PSPDEV}/psp/include/ -G0" LDFLAGS="-L${PSPDEV}/psp/sdk/lib -L  ${PSPDEV}/psp/lib -lc -lpspuser -lpspkernel" CFLAGS="-I${PSPDEV}/psp/sdk/include" ./configure -host=psp

comment out HAVE_PWD_H and DB_HAVE_NO_POWF from config.h

make 

cd src && psp-gcc -L${PSPDEV}/psp/sdk/lib -L${PSPDEV}/psp/lib -L${PSPDEV}/psp/bin -o dosbox dosbox.o cpu/libcpu.a debug/libdebug.a dos/libdos.a fpu/libfpu.a hardware/libhardware.a gui/libgui.a ints/libints.a shell/libshell.a -lm hardware/serialport/libserial.a libs/gui_tk/libgui_tk.a hardware/mame/libmame.a misc/libmisc.a -lSDLmain -lSDL   -lm -lGL -lm -lpspvfpu -L/usr/local/pspdev/psp/sdk/lib -L/usr/local/pspdev/psp -lpspdebug -lpspgu -lpspctrl -lpspge -lpspdisplay -lpsphprm -lpspsdk -lpsprtc -lpspaudio -lpsputility -lpspnet_inet -lpspirkeyb -lpsppower -lc -lpspuser -lpspdebug -lpspgu -lpspctrl -lpspdisplay -lpspge -lpspsdk -lpsprtc -lpng -lpng15 -lpspaudio -lstdc++ -lpspirkeyb -lc -lpspnet -lpspnet_inet -lpsppower -lpsputility -lpspuser -lpspkernel -specs=${PSPDEV}/psp/sdk/lib/prxspecs -Wl,-T${PSPDEV}/psp/sdk/lib/linkfile.prx,-q && psp-fixup-imports dosbox && psp-prxgen dosbox dosbox.prx && mksfo "DOSBox PSP" PARAM.SFO && pack-pbp EBOOT.PBP PARAM.SFO NULL NULL NULL NULL NULL dosbox.prx NULL && cd ..
