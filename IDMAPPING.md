# MAVLink-M message ID renumber: 60xxx to 54xxx

**Status: provisional.** The dialect has been moved out of the 60000-60099 band
(which is allocated to the `storm32` and `AVSSUAS` dialects in the upstream MAVLink
repo) into **54000-54099**, an unallocated block. 54000 is the front of the
maintainers' own "next to allocate" corridor (54000-60000 per `all.xml`).

These IDs are **placeholders for development only** until an official message-ID range
is granted by the MAVLink project (GitHub issue on `mavlink/mavlink`). If the granted
range differs, renumber once more to the granted block. The wire structure, field
layout, and `track_uid` correlation spine are unchanged - only the integer IDs moved.

## Messages (base dialect)

| Name | Old ID | New ID |
| --- | --- | --- |
| TRACK_IDENTITY | 60000 | 54000 |
| TARGET_CUE | 60001 | 54001 |
| TARGET_HANDOVER | 60002 | 54002 |
| PARTICIPANT_POSITION | 60003 | 54003 |
| MAVLINK_M_ACK | 60004 | 54004 |
| TARGET_COORD | 60010 | 54010 |
| TARGET_SET_COORD | 60011 | 54011 |
| TARGET_BOX_COORD | 60012 | 54012 |
| TARGET_AUTHORIZATION | 60013 | 54013 |
| FIRES | 60020 | 54020 |
| SPLASH_CORRECTION | 60021 | 54021 |
| BATTLE_DAMAGE_ASSESSMENT | 60022 | 54022 |
| ENGAGEMENT_DIRECTIVE | 60023 | 54023 |
| CALL_FOR_FIRE | 60024 | 54024 |
| ESAD_STATE | 60030 | 54030 |
| ESAD_ARMING | 60031 | 54031 |
| ESAD_CONFIG | 60032 | 54032 |
| STORE_STATUS | 60033 | 54033 |
| STORE_SENSOR_STATUS | 60034 | 54034 |
| STORE_MUNITION | 60035 | 54035 |
| LOITER_MUNITION_CONTROL | 60036 | 54036 |
| RWS_POSE | 60040 | 54040 |
| RWS_STATE | 60041 | 54041 |
| SENSOR_TASKING | 60050 | 54050 |

Rule: **new = old - 6000**. Internal block structure is preserved.

## MAV_CMD (base dialect)

| Name | Old value | New value |
| --- | --- | --- |
| MAV_CMD_MAVLINK_M_STORE_ARM | 60100 | 54090 |
| MAV_CMD_MAVLINK_M_STORE_RUN_BIT | 60101 | 54091 |
| MAV_CMD_MAVLINK_M_STORE_REQUEST_STATUS | 60102 | 54092 |
| MAV_CMD_MAVLINK_M_STORE_SET_DECEL_THRESHOLD | 60103 | 54093 |

Commands are placed at 54090-54093 to keep them inside the single 54000-54099 window
alongside the messages (messages occupy 54000-54050; 54090+ leaves growth room
between).

## Extensions dialect

| Name | Old ID | New ID |
| --- | --- | --- |
| CAS_9LINE | 60060 | 54060 |
| TERMINAL_CONTROL | 60061 | 54061 |

## Range check

54000-54099 was verified against every allocated and reserved range in the canonical
`mavlink/mavlink` `all.xml`: **no collision** with common, ASLUAV, uAvionix,
ardupilotmega, icarous, cubepilot, ras_a, csAirLink, marsh, stemstudios, storm32,
AVSSUAS, or the reserved 52100-52499 / 53000-53999 blocks.

## Prior Dronecode military.xml IDs

The Dronecode/mavlink-military repo previously carried an 11-message
preliminary spec at 53000-53010, inside the reserved 53000-53999 band noted
above. Those messages map to the new IDs as follows:

| Name | Old ID (military.xml) | New ID |
| --- | --- | --- |
| TARGET_SET_COORD | 53000 | 54011 |
| TARGET_BOX_COORD | 53001 | 54012 |
| TARGET_COORD | 53002 | 54010 |
| FIRES | 53003 | 54020 |
| SPLASH_CORRECTION | 53004 | 54021 |
| TARGET_HANDOVER | 53005 | 54002 |
| BATTLE_DAMAGE_ASSESSMENT | 53006 | 54022 |
| ESAD_STATE | 53007 | 54030 |
| ESAD_ARMING | 53008 | 54031 |
| RWS_POSE | 53009 | 54040 |
| RWS_STATE | 53010 | 54041 |

The 53000-53999 reservation in upstream all.xml (added 2026-02-26, contact
hamishwillee@gmail.com) may in fact be held for this dialect; if the
maintainers confirm that, renumbering from 54xxx into 53000-53099 is a
mechanical shift of 1000.

## Coordination note

Documentation (specification, guide, change-list, extensions guide, demo spec) still
references the old 60xxx IDs. Those docs are being held rather than regenerated,
because the range is provisional - they will be regenerated once against the final
allocated range. Until then, this table is the source of truth for the ID mapping.
