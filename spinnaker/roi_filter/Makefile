# If SPINN_DIRS is not defined, this is an error!
ifndef SPINN_DIRS
    $(error SPINN_DIRS is not set.  Please define SPINN_DIRS (possibly by running "source setup" in the spinnaker package folder))
endif

APP = roi_filter
SOURCES = roi_filter.c
APP_OUTPUT_DIR = ../cbin/

SOURCE_DIRS = src/
MODIFIED_DIR = modified_src/
BUILD_DIR = build/


#MAKEFILE_PATH := $(abspath $(lastword $(MAKEFILE_LIST)))
#CURRENT_DIR := $(dir $(MAKEFILE_PATH))
#SOURCE_DIR := $(abspath $(CURRENT_DIR))
#SOURCE_DIRS += $(SOURCE_DIR)
#APP_OUTPUT_DIR := $(abspath $(CURRENT_DIR))/../binaries/

include $(SPINN_DIRS)/make/local.mk
