==making patches==

apt-get install --no-install-recommends nvidia-$R
cd /usr/src
cp -a nvidia-$R-$V nvidia-$R-$V.fix
edit nvidia-$R-$V.fix
diff -urN nvidia-$R-$V nvidia-$R-$V.fix > nvidia-patches/nvidia-$R_kernel_$K.patch

edit /etc/dkms/nvidia-$R-$V.conf

patch path:
"../../../../../../../usr/src/nvidia-patches/nvidia-$R_kernel-$K.patch"

check:
sudo dkms build -m nvidia-$R -v $V -k $K
