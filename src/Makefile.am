# Copyright (C) 2007, 2008, 2009, 2010, 2011, 2012 Her Majesty the
# Queen in Right of Canada (Communications Research Center Canada)

# This file is part of ODR-DabMod.
#
# ODR-DabMod is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as
# published by the Free Software Foundation, either version 3 of the
# License, or (at your option) any later version.
#
# ODR-DabMod is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
# 
# You should have received a copy of the GNU General Public License
# along with ODR-DabMod.  If not, see <http://www.gnu.org/licenses/>.

if IS_GIT_REPO
GITVERSION_FLAGS = -DGITVERSION="\"`git describe`\""
else
GITVERSION_FLAGS =
endif

if HAVE_SSE
SIMD_CFLAGS = -msse -msse2
else
SIMD_CFLAGS =
endif

bin_PROGRAMS = odr-dabmod

if USE_KISS_FFT
FFT_DIR=$(top_builddir)/lib/kiss_fft129
FFT_INC=-I$(FFT_DIR) -I$(FFT_DIR)/tools
FFT_SRC=$(FFT_DIR)/kiss_fft.c \
		$(FFT_DIR)/kiss_fft.h \
		$(FFT_DIR)/tools/kiss_fftr.c \
		$(FFT_DIR)/tools/kiss_fftr.h \
		kiss_fftsimd.c \
		kiss_fftsimd.h
FFT_FLG=-ffast-math

.PHONY: kiss_fft129 reed-solomon-4.0

DabModulator.cpp: $(FFT_DIR)

BUILT_SOURCES: $(FFT_DIR)

FFT_LDADD=

$(FFT_DIR):
	if [ ! -e $(FFT_DIR) ]; then \
		tar xzf $(top_srcdir)/lib/kiss_fft129.tar.gz -C $(top_builddir)/lib; \
	fi

else
FFT_LDADD=
FFT_DIR=
FFT_INC=
FFT_SRC=
FFT_FLG=
endif

odr_dabmod_CPPFLAGS = -Wall \
					  $(FFT_INC) $(FFT_FLG) $(SIMD_CFLAGS) $(GITVERSION_FLAGS)
odr_dabmod_LDADD    = $(FFT_LDADD)
odr_dabmod_SOURCES  = DabMod.cpp \
					  PcDebug.h \
					  porting.c porting.h \
					  DabModulator.cpp DabModulator.h  \
					  Buffer.cpp Buffer.h \
					  ModCodec.cpp ModCodec.h \
					  ModPlugin.cpp ModPlugin.h \
					  ModFormat.cpp ModFormat.h \
					  EtiReader.cpp EtiReader.h \
					  Eti.cpp Eti.h \
					  FicSource.cpp FicSource.h \
					  FIRFilter.cpp FIRFilter.h \
					  ModInput.cpp ModInput.h \
					  PuncturingRule.cpp PuncturingRule.h \
					  PuncturingEncoder.cpp PuncturingEncoder.h \
					  SubchannelSource.cpp SubchannelSource.h \
					  Flowgraph.cpp Flowgraph.h \
					  GainControl.cpp GainControl.h \
					  OutputMemory.cpp OutputMemory.h \
					  OutputZeroMQ.cpp OutputZeroMQ.h \
					  TimestampDecoder.h TimestampDecoder.cpp \
					  OutputUHD.cpp OutputUHD.h \
					  ModOutput.cpp ModOutput.h \
					  InputMemory.cpp InputMemory.h \
					  InputFileReader.cpp InputZeroMQReader.cpp InputReader.h \
					  OutputFile.cpp OutputFile.h \
					  FrameMultiplexer.cpp FrameMultiplexer.h \
					  ModMux.cpp ModMux.h \
					  PrbsGenerator.cpp PrbsGenerator.h \
					  BlockPartitioner.cpp BlockPartitioner.h \
					  QpskSymbolMapper.cpp QpskSymbolMapper.h \
					  FrequencyInterleaver.cpp FrequencyInterleaver.h \
					  PhaseReference.cpp PhaseReference.h \
					  DifferentialModulator.cpp DifferentialModulator.h \
					  NullSymbol.cpp NullSymbol.h \
					  SignalMultiplexer.cpp SignalMultiplexer.h \
					  CicEqualizer.cpp CicEqualizer.h \
					  OfdmGenerator.cpp OfdmGenerator.h \
					  GuardIntervalInserter.cpp GuardIntervalInserter.h \
					  Resampler.cpp Resampler.h \
					  ConvEncoder.cpp ConvEncoder.h \
					  TimeInterleaver.cpp TimeInterleaver.h \
					  ThreadsafeQueue.h \
					  Log.cpp Log.h \
					  RemoteControl.cpp RemoteControl.h \
					  FormatConverter.cpp FormatConverter.h \
					  zmq.hpp

nodist_odr_dabmod_SOURCES = $(FFT_SRC)

dist_bin_SCRIPTS = crc-dwap.py

if USE_KISS_FFT
EXTRA_DIST = kiss_fftsimd.c kiss_fftsimd.h

clean-local:
	rm -rf $(FFT_DIR)

endif

