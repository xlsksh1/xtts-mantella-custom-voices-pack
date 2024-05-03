## XTTS Mantella Custom Voices Pack

This is a repository containing `latent_speaker` JSON files of trained voiced data. The main purpose is to have a repository full of custom voices for Skyrim or Fallout4, and have it synced with a build that can be XTTS Mantella server that can be deployed in the cloud.

## Usage Locally
- 

## Usage Cloud

Anytime a new file is added or updated within the `latent_speaker_folder` a new build will be made. The latest build will always be used when deploying a `xtts-mantella-custom-voices-pack` build in the cloud. 

This means if you wish to run your own custom voices in a cloud server, all you have to do is test your custom voice files in game and then add your generated `latent_speaker` json to this repository. After a few minutes the new build is made, so just create a new runpod.io pod or an instance of whatever service you use.

Feel free to make pull request with your trained files, or if you are a contributor then directly push your files to main whenever.

### Runinng in runpod.io

Click the following URL to setup a new runpod.io pod. It will setup the XTTS Mantella API server along all the custom voice files found in this repo.

- [runpod template](https://runpod.io/console/deploy?template=kv0kqgd8oi&ref=u2snoorq)

For more information, refer to Mantella XTTS docs: https://art-from-the-machine.github.io/Mantella/pages/installation.html#text-to-speech

### Running else where 

If you wish to run this somewhere else, you can just grab the latest Docker build: `docker pull koukidevdocks/xtts-mantella-custom-voices-pack:main`.

## Reference

Mantella: https://art-from-the-machine.github.io/Mantella
  - Repo: 
XTTS Mantella API Server: https://www.nexusmods.com/skyrimspecialedition/mods/113445
  - Repo: https://github.com/Haurrus/xtts-api-server-mantella/tree/local_mantella_api
  - Note the build will grab the latest XTTS Mantella API Server docker build, which contains voices for the original SKyrim and Fallout games. If you wish to edit those orginal files, refer there.