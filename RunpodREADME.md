Docker image of [xtts-api-server-mantella](https://github.com/koukisdevki/xtts-mantella-custom-voices-pack) with custom voice model latents created by the community for Skyrim and Fallout 4.

Intended for use with Mantella - Bring NPCs to Life with AI. If you wish to create an xtts mantella server without community custom voices, you can find the link [here](https://art-from-the-machine.github.io/Mantella/pages/installation.html#text-to-speech). 

Once this template is running in a pod, set `tts_service` in `[Speech]` to `"XTTS"` and `xtts_url` in `[Speech.Advanced]` to:

`https://{POD_ID}-8020.proxy.runpod.net`

in `MantellaSoftware/config.ini`, with `{POD-ID}` being the ID of the running pod.