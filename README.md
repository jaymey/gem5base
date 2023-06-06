# gem5base
Base Gem5 Running Ubuntu Full System

Clone this repo
Then clone a gem5 repo into it such that it resides at gem5base/gem5 alongside gem5base/disk-image
Add the provided x86-ubuntu-run-with-kvm.py into the configs folder of gem5 (feel free to rename the script)

Build gem5:
cd gem5
scons build/{ISA}/gem5.{variant} -j {cpus}
(scons build X86/gem5.opt -j8)


Build m5 utils:
cd gem5/util/m5
scons build/x86/out/m5

Build m5term:
cd gem5/util/term
make

Build the disk image:
cd gem5base/disk-image
./build.sh


Once everything is built, run the script using:
./build/X86/gem5.opt {PATH TO SCRIPT}/x86-ubuntu-run-with-kvm.py --image {FULL PATH TO BUILT IMAGE} --partition 1

Find the line in the full system boot up window that reads as:
"board.pc.com_1.device: Listening for connections on port {PORT NUMBER}"

In another terminal window run m5term:
cd gem5/util/term
./m5term localhost {PORT NUMBER}

You should be able to see the command line of the full system. Congratulations!
