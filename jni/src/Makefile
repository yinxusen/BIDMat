include Makefile.incl

MKL_OBJS=BIDMat_CBLAS.$(OBJ) BIDMat_SPBLAS.$(OBJ) BIDMat_LAPACK.$(OBJ) \
         BIDMat_VML.$(OBJ) BIDMat_VSL.$(OBJ)

CUDA_OBJS=BIDMat_CUMAT.$(OBJ) MatKernel.$(OBJ) 

.SUFFIXES: .$(OBJ) .c

all: $(LIBPREPEND)bidmatmkl$(LIBAPPEND) $(LIBPREPEND)bidmatcuda$(LIBAPPEND)

$(LIBPREPEND)bidmatmkl$(LIBAPPEND): $(MKL_OBJS)
	$(LD) $(LDFLAGS) $(MKL_OBJS) $(MKL_LIBS) $(OUTFLG)$@

$(LIBPREPEND)bidmatcuda$(LIBAPPEND): $(CUDA_OBJS)
	$(LD) $(LDFLAGS) $(CUDA_OBJS) $(CUDA_LIBS) $(OUTFLG)$@

%.$(OBJ) : %.c
	$(CC) $(CPPFLAGS) $(LAPACK_INCLUDES) $(CFLAGS) $*.c

%.$(OBJ) : %.cpp
	$(CC) $(CPPFLAGS) $(LAPACK_INCLUDES) $(CFLAGS) $*.cpp

%.$(OBJ) : %.cu
	$(NVCC) $(NVCCFLAGS) $*.cu

install: all
	cp $(LIBPREPEND)bidmatmkl$(LIBAPPEND)  ../../lib/win64
	cp $(LIBPREPEND)bidmatcuda$(LIBAPPEND) ../../lib/win64

clean:
	rm -f *.$(OBJ) *$(LIBAPPEND) *.pdb *.exp *.lib

distclean: clean
	rm -f *$(LIBAPPEND) *.exp *.lib *.jnilib Makefile.incl
