# neuropixel_preprocessing: spike-sorting, event extraction, synchronization using [Kilosort4](https://github.com/MouseLand/Kilosort)

This is a pipeline which spike-sorts neuropixel 1.0 data aquired with [SpikeGLX](https://billkarsh.github.io/SpikeGLX/) and task control via either [NIMH MonkeyLogic](https://monkeylogic.nimh.nih.gov/index.html) or [PsychToolbox](https://psychtoolbox.org/). It is geared towards NHP users. 

## Automated spike-sorting and basic quality metrics
`npx_ks4_pipeline.ipynb` uses [Kilosort 4](https://github.com/MouseLand/Kilosort) to sort your data, compute basic quality metrics for each of the putative unit, and map all data streams to a common timeline.

To use this notebook straight out of the box, you'll need to have Kilosort 4 installed on your computer. This pipeline is optimized for recordings made with [SpikeGLX](https://billkarsh.github.io/SpikeGLX/) where each probe has its own folder.

If you've got everything set up as described above, all you need to do the run the notebook is modify a  path variable in the second code cell. Specifically:
- `base_folder`: path to the folder containing your recording data (the one that has the imec0 and imec1 sub-directories in it). 

If you are recording from multiple brain areas, you can also modify the `brain_areas` variable such that the first element is the brain area you lowered the `imec0` probe into and the second element is the brain area you lowered the `imec1` probe into. Extend this list to as many brain areas as you have probes. 

## Extracting event codes and mapping your data to a common timeline

`npx_ks4_pipeline.ipynb` also extracts the event codes and edges of synchronization pulses across all of your data streams and places all of your spike/event data onto a common timeline. 

**<ins>Note:</ins>** For the nidaq stream, it assumes that you are using analog channel 0 as your sync_channel - in other words, that you have run a coax cable from the IMEC card on the NI-chassis to analog channel 0 on your nidaq board. 

## For NHP users:
I also provide a channel map for the NHP neuropixel probes. This is the default of the `channel_map` variable set in the second code cell. To use this channel map, you need to place `neuropixPrimate_kilosortChanMap.mat` in the appropriate directory so kilosort can find it. Assuming you are using a Windows machine, it should be placed at e.g. `C:\Users\Thomas Elston\.kilosort\probes`

**<ins>Note:</ins>**  to see this directory, you need to make the hidden folders visible at `C:\Users\your_directory\`
