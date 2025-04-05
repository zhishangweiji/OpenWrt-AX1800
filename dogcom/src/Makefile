# 使用 OpenWrt 的交叉编译器（通过环境变量覆盖）
CC = $(TARGET_CC)
TARGET = dogcom
INSTALL_DIR = $(DESTDIR)/usr/bin

# 添加 OpenWrt 头文件和库路径
CFLAGS += -I$(STAGING_DIR)/target-*/usr/include
LDFLAGS += -L$(STAGING_DIR)/target-*/usr/lib -lpcap -lssl -lcrypto

# 调试选项
ifeq ($(debug), y)
	CFLAGS += -DDEBUG -g
else
	CFLAGS += -Os -s
endif

# 强制加密（按需启用）
ifeq ($(force_encrypt), y)
	CFLAGS += -DFORCE_ENCRYPT
endif

# 标准编译选项
CFLAGS += -std=gnu99 -Wall -Wextra -Werror

SOURCES = $(wildcard *.c) $(wildcard libs/*.c)
OBJS    = $(patsubst %.c, %.o, $(SOURCES))

$(TARGET): $(OBJS)
	$(CC) $(CFLAGS) $(OBJS) $(LDFLAGS) -o $@

all: $(TARGET)

install: $(TARGET)
	mkdir -p $(INSTALL_DIR)
	cp $(TARGET) $(INSTALL_DIR)/

clean:
	rm -f $(OBJS) $(TARGET)

.PHONY: all clean install
