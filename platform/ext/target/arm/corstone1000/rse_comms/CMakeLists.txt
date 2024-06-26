#-------------------------------------------------------------------------------
# Copyright (c) 2022-2024, Arm Limited. All rights reserved.
#
# SPDX-License-Identifier: BSD-3-Clause
#
#-------------------------------------------------------------------------------

target_include_directories(platform_s
    PUBLIC
        .
)

target_sources(platform_s
    PRIVATE
        rse_comms.c
        rse_comms_hal.c
        rse_comms_queue.c
        rse_comms_protocol.c
        rse_comms_protocol_embed.c
)

target_compile_definitions(platform_s
    PRIVATE
        RSE_COMMS_MAX_CONCURRENT_REQ=1
        RSE_COMMS_PROTOCOL_EMBED_ENABLED
        $<$<BOOL:${CONFIG_TFM_HALT_ON_CORE_PANIC}>:CONFIG_TFM_HALT_ON_CORE_PANIC>
)

# For spm_log_msgval
target_link_libraries(platform_s
    PRIVATE
        tfm_spm
        tfm_sprt
)
