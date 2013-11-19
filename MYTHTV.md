# VDPAU for MythTV 

## VDPAU Calls from MythTV

The following calls are required by MythTV to fully operate using VDPAU

### Bitmap Surface
* vdp_bitmap_surface_create -
* vdp_bitmap_surface_destroy - 
* vdp_bitmap_surface_put_bits_native -

### Decoder
* vdp_decoder_create +
* vdp_decoder_destroy +
* vdp_decoder_query_capabilities +
* vdp_decoder_render +

### Device
* vdp_device_destroy +
* vdp_preemption_callback_register +
* vdp_get_api_version +
* vdp_get_error_string +
* vdp_get_information_string +
* vdp_get_proc_address +

### Output Surface
* vdp_output_surface_create +
* vdp_output_surface_destroy +
* vdp_output_surface_get_bits_native -
* vdp_output_surface_get_parameters +
* vdp_output_surface_render_bitmap_surface -
* vdp_output_surface_render_output_surface -

### Presentation Queue
* vdp_presentation_queue_block_until_surface_idle ?
* vdp_presentation_queue_create +
* vdp_presentation_queue_destroy +
* vdp_presentation_queue_display +
* vdp_presentation_queue_set_background_color +
* vdp_presentation_queue_target_destroy +

### Video Mixer
* vdp_video_mixer_create +
* vdp_video_mixer_destroy +
* vdp_video_mixer_query_feature_support (no features supported) ?
* vdp_video_mixer_render +?
* vdp_video_mixer_set_attribute_values (has no attributes)
* vdp_video_mixer_set_feature_enables (has no features)

### Video Surface
* vdp_video_surface_create +
* vdp_video_surface_destroy +
* vdp_video_surface_get_bits_y_cb_cr -
* vdp_video_surface_get_parameters +
* vdp_video_surface_put_bits_y_cb_cr +

## Unimplemented / Not Fully Supported

### vdp_video_mixer_render
Does not support TOP/BOTTOM field

### vdp_video_mixer_query_feature_support
Checks each scaling level feature is supported

    VDP_VIDEO_MIXER_FEATURE_HIGH_QUALITY_SCALING_L1 + (0..9)

### vdp_video_mixer_set_attribute_values

    VDP_VIDEO_MIXER_ATTRIBUTE_SHARPNESS_LEVEL
    VDP_VIDEO_MIXER_ATTRIBUTE_NOISE_REDUCTION_LEVEL
    VDP_VIDEO_MIXER_ATTRIBUTE_SKIP_CHROMA_DEINTERLACE
    VDP_VIDEO_MIXER_ATTRIBUTE_BACKGROUND_COLOR

### vdp_video_mixer_set_feature_enables

    VDP_VIDEO_MIXER_FEATURE_DEINTERLACE_TEMPORAL
    VDP_VIDEO_MIXER_FEATURE_DEINTERLACE_TEMPORAL_SPATIAL
    VDP_VIDEO_MIXER_FEATURE_INVERSE_TELECINE
    VDP_VIDEO_MIXER_FEATURE_NOISE_REDUCTION
    VDP_VIDEO_MIXER_FEATURE_SHARPNESS
    VDP_VIDEO_MIXER_FEATURE_HIGH_QUALITY_SCALING_L1 + (0..9) (best from query)

with parameters

    VdpVideoMixerParameter parameters[] = {
        VDP_VIDEO_MIXER_PARAMETER_VIDEO_SURFACE_WIDTH,
        VDP_VIDEO_MIXER_PARAMETER_VIDEO_SURFACE_HEIGHT,
        VDP_VIDEO_MIXER_PARAMETER_CHROMA_TYPE,
        VDP_VIDEO_MIXER_PARAMETER_LAYERS,
    };

    type = VDP_CHROMA_TYPE_420;
    layers = 0 or 2;
    
    void const * parameter_values[] = { &width, &height, &type, &layers};
