# SM Houdini Redshift3D ACES Workflow Convenience Tools

Several tools are included in this folder. 
- COPS: sm_rgb_to_acescg: this hda converts the input linear rgb image to acescg. It's basically a wrapper around a cop2filter vop
- COPS: sm_export_aces_texture: this hda is a wrapper around the sm_rgb_to_acescg that allows you to specify a path to a texture, and exports a new exr in acescg colourspace.
- SOPS: sm_sop_cd_to_acescg: this hda wraps a vop sop that converts Cd into the acescg colourspace. Rarely used, only when I'm rendering Cd directly
- Shelf: SM Convert Texture to ACES : This shelf tool converts textures loaded into the RS Dome Light or RS Texture vop into a .exr in the acescg colourspace, and updates the name.

ACES Workflow quick refresher (30th May 2020)
- Download ACES package (https://opencolorio.org/)
- Set OCIO env variable to point to config.ocio
- In Houdini: Viewport right list of icons, scroll to very bottom, right click on Display options, enable Colour correction. Choose view transform (sRRB, Rec709, P3-DCI etc)
- In Redshift Renderview: Display Mode: OCIO, set view transform as above. 
- Fusion - Enable LUT, choose OCIO Colourspace. Source space acescg, output space is your view transform.
- Resolve - project settings, color management, color science: Change to acescc. Choose appropriate transforms. When applying luts, drag OpenFX ACES Transform on a new node, convert aces to r709, another node to apply lut, then another node the inverse of first node to return to aces color space.
