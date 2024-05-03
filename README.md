## XTTS Mantella Custom Voices Pack

This is a repository containing `latent_speaker` JSON files of trained voiced data. The main purpose is to have a repository full of custom voices for Skyrim or Fallout4, and have this repo always be in sync with a build that can be deployed in the cloud as a XTTS Mantella server.

## Usage Locally

Simply copy all the files from the `latent_speaker_folder` into your xtts-mantella folder `latent_speaker_folder` and start the xtts server.

## Usage Cloud

Anytime a new file is added or updated within the `latent_speaker_folder` a new build will be made automatically. The latest build will always be used when deploying a `xtts-mantella-custom-voices-pack` build in the cloud. 

This means if you wish to run your own custom voices in a cloud server, all you have to do is test your custom voice files in game and then add your generated `latent_speaker` json to this repository. After a few minutes, the new build will be made so just create a new runpod.io pod or an instance of whatever service you use.

Feel free to make pull request with your trained files, or if you are a contributor then directly push your files to main whenever.

### Runinng in runpod.io

Click the following URL to setup a new runpod.io pod. It will setup the XTTS Mantella API server along all the custom voice files found in this repo.

- [runpod template](https://runpod.io/console/deploy?template=kv0kqgd8oi&ref=u2snoorq)

It is more than enough to simply choose the cheapest option, as of date a 3070, on community cloud.

For more information, refer to Mantella XTTS docs: https://art-from-the-machine.github.io/Mantella/pages/installation.html#text-to-speech

### Running else where 

If you wish to run this somewhere else, you can just grab the latest Docker build: `docker pull koukidevdocks/xtts-mantella-custom-voices-pack:main`.

## List of Custom NPCs

Below is a list of NPCS. If you do contribute to the latent_speaker, please be sure to add the NPC here as well for documentation.

### Skyrim

- Sofia: https://www.nexusmods.com/skyrimspecialedition/mods/2180
- Recorder: https://www.nexusmods.com/skyrimspecialedition/mods/4718
- Lydia (Improved Follower Dialogue): https://www.nexusmods.com/skyrimspecialedition/mods/38473

## Training your own Custom NPCs

Training your own custom NPCs is really easy, its actually one of the biggest selling points of `XTTS`. 

I'll be using Skyrim to explain. These are the instructions for the current Mantella and XTTS-Mantella-Server version as of time of writting. 

1. Find the NPC files of the NPC you want to target, you will need the in-game name of the NPC and its voice `.wav` sound voice files for training. Loose files will have these `.wav` files under `{Mod File}\Sound\Voice\{Mod}.esp\{npc_voicetype}\` in the form of `.fuz` files that must be converted to `.wav`. If your NPC is bundled within a `.bsa` file, use [BAE](https://www.nexusmods.com/skyrimspecialedition/mods/974/) to extract them to loose files.
2. Download and install [XTTS Mantella API Server](https://www.nexusmods.com/skyrimspecialedition/mods/113445). Make sure to also download the `gradio mantella request test` files which you will use in step 6, and place it inside this XTTS server's folder too.
3. Prepare your `.wav` files by extracting them from your `.fuz` files. Use [Yakitori Audio Converter](https://www.nexusmods.com/skyrimspecialedition/mods/17765) to achieve this. Simple find the npc voice folder with all of the `.fuz` files, and batch convert them to `.wav`.
4. Within the XTTS mantella root folder, you will need to create a `speakers\{lang}\{npc_voice_name}` folder, where `{lang}` is the target language of your file and `{npc_voice_name}` is your NPC's `voice_model` as specified within Mantell `.csv`. Carefully select your `.wav` files and place them in this folder. If you are lazy just put all `.wav` of your NPC in this folder.
   - i.e `speakers\en\sofia` will contain all of the chosen sofia `.wav` files. 
   - IMPORTANT: You want the `npc_voice_name` to be the `voice_model` within Mantella's `data\skyrim\skyrim_characters.csv` folder and NOT the voicetype or voicetypefolder. This is what Mantella currently uses as the NPC name when calling XTTS. So be sure to look up with voice model using your NPC's name in the CSV. 
5. Run `xtts-api-server-mantella.exe` so it boots up the server and trains your voice. XTTS will generate the trained latent speaker JSON file under `latent_speaker_folder\{lang}\{npc_voice_name}.json`. After it generates the `.json` file and the xtts server loads. Check your files that this `.json` file was generated.
6. Test your voice by running the following from the xtts server root folder using your shell/terminal: `.\gradio_xtts_mantella_request.exe --text {text} --language {lang} --speaker_wav {npc_voice_name}`. An `output` .wav file is generated which contains the text you are testing. Make sure the xtts is running while running this command. 
   - Ex: `.\gradio_xtts_mantella_request.exe --text "Hello There Dragonborn, where shall we go tonight? Where ever it is, I just want some ale." --language en --speaker_wav sofia`
7. If you are not happy with the generated sample voice, you may delete the generated `latent_speaker_folder` JSON file. Repeats steps 4-6 until you are happy with your voice samples.
8. IMPORTANT!! Make sure to test your files locally using a local XTTS within your game. Boot up skyrim and find your NPC, then talk to them using the Mantella spell. 
9. If everything is fine, you may then finally push your `json` latent files to this repository. Create a pull-request with these files. The file is what was generated in step 5, `latent_speaker_folder\{lang}\{npc_voice_name}.json`.

## Reference

Mantella: https://art-from-the-machine.github.io/Mantella
  - Repo: https://github.com/art-from-the-machine/Mantella
  
XTTS Mantella API Server: https://www.nexusmods.com/skyrimspecialedition/mods/113445
  - Repo: https://github.com/Haurrus/xtts-api-server-mantella/tree/local_mantella_api
  - Note the build will grab the latest XTTS Mantella API Server docker build, which contains voices for the original SKyrim and Fallout games. If you wish to edit those orginal files, refer there.