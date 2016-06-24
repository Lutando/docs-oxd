[TOC]

# Libraries


## Protocol support table version 2.4.4


| Commands/features        | oxD Server    | oxd-java | oxd-php | oxd-python | oxd-node | oxd-ruby | oxd-charp |
| ------------------------ |---------------| -------- | ------- | ---------- | -------- | -------- | --------- |
| register_site            |     *+*       |    *+*   |   *+*   |    *+*     |     ?    |     ?    |    *+*    |
| update_site_registration |     *+*       |    *+*   |   *+*   |    *+*     |     ?    |     ?    |    *+*    |
| get_authorization_url    |     *+*       |    *+*   |   *+*   |    *+*     |     ?    |     ?    |    *+*    |
| get_tokens_by_code       |     *+*       |    *+*   |   *+*   |    *+*     |     ?    |     ?    |    *+*    |
| get_user_info            |     *+*       |    *+*   |   *+*   |    *+*     |     ?    |     ?    |    *+*    |
| uma_rs_protect           |     *+*       |    *+*   |   *+*   |     ?      |     ?    |     ?    |    *-*    |
| uma_rs_check_access      |     *+*       |    *+*   |   *+*   |     ?      |     ?    |     ?    |    *-*    |
| uma_rp_get_rpt           |     *+*       |    *+*   |   *+*   |     ?      |     ?    |     ?    |    *-*    |
| uma_rp_authorize_rpt     |     *+*       |    *+*   |   *+*   |     ?      |     ?    |     ?    |    *-*    |
| uma_rp_get_gat           |     *+*       |    *+*   |   *-*   |     ?      |     ?    |     ?    |    *-*    |
| Interop UMA RS Test      |no for server  |    *-*   |   *-*   |     ?      |     ?    |     ?    |    *-*    |
| Interop UMA RP Test      |no for server  |    *-*   |   *-*   |     ?      |     ?    |     ?    |    *-*    |


Under "Interop UMA Test" means this test description: https://ox.gluu.org/doku.php?id=oxd:testtool
