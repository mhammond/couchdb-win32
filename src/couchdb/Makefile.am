## Licensed under the Apache License, Version 2.0 (the "License"); you may not
## use this file except in compliance with the License.  You may obtain a copy
## of the License at
##
##   http://www.apache.org/licenses/LICENSE-2.0
##
## Unless required by applicable law or agreed to in writing, software
## distributed under the License is distributed on an "AS IS" BASIS, WITHOUT
## WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.  See the
## License for the specific language governing permissions and limitations under
## the License.

ICU_LOCAL_FLAGS = $(ICU_LOCAL_CFLAGS) $(ICU_LOCAL_LDFLAGS)
if WINDOWS
ICU_LOCAL_LIBS=-licuuc -licudt -licuin
else
ICU_LOCAL_LIBS=-licuuc -licudata -licui18n
endif

# devdocdir = $(localdocdir)/developer/couchdb
couchlibdir = $(localerlanglibdir)/couch-$(version)
couchprivdir = $(couchlibdir)/priv
couchprivlibdir = $(couchlibdir)/priv/lib
couchincludedir = $(couchlibdir)/include
couchebindir = $(couchlibdir)/ebin

couchprivlib_LTLIBRARIES = couch_erl_driver.la
couch_erl_driver_la_SOURCES = couch_erl_driver.c
couch_erl_driver_la_LDFLAGS = -module -avoid-version $(ICU_LOCAL_FLAGS)
couch_erl_driver_la_CFLAGS = $(ICU_LOCAL_FLAGS)
couch_erl_driver_la_LIBADD = $(ICU_LOCAL_LIBS)

locallibbin_PROGRAMS = couchjs
couchjs_SOURCES = couch_js.c curlhelper.c curlhelper.h
couchjs_LDFLAGS = $(CURL_LDFLAGS)
couchjs_CFLAGS = $(CURL_CFLAGS)
couchjs_LDADD = $(CURL_LDFLAGS)

if WINDOWS
priv_couchspawnkillable_SOURCES = priv/couchspawnkillable_win.c
couchpriv_PROGRAMS = priv/couchspawnkillable
couch_erl_driver_la_LDFLAGS += -no-undefined

# copy ICU dlls for the erlang driver
dist_couch_erl_driver_la_DATA=$(ICU_LOCAL_BIN)/icuuc42.dll $(ICU_LOCAL_BIN)/icudt42.dll $(ICU_LOCAL_BIN)/icuin42.dll
couch_erl_driver_ladir=$(bindir)
endif

couchinclude_DATA = couch_db.hrl

couchebin_DATA = $(compiled_files)

couchpriv_SCRIPTS = priv/couchspawnkillable

# dist_devdoc_DATA = $(doc_base) $(doc_modules)

CLEANFILES = $(compiled_files) $(doc_base)

# CLEANFILES = $(doc_modules) edoc-info

source_files = \
    couch_btree.erl \
    couch_batch_save.erl \
    couch_batch_save_sup.erl \
    couch_config.erl \
    couch_config_writer.erl \
    couch_db.erl \
    couch_db_update_notifier.erl \
    couch_db_update_notifier_sup.erl \
    couch_doc.erl \
    couch_event_sup.erl \
    couch_external_manager.erl \
    couch_external_server.erl \
    couch_file.erl \
    couch_httpd.erl \
    couch_httpd_db.erl \
    couch_httpd_external.erl \
    couch_httpd_show.erl \
    couch_httpd_view.erl \
    couch_httpd_misc_handlers.erl \
    couch_httpd_stats_handlers.erl \
    couch_key_tree.erl \
    couch_log.erl \
    couch_os_process.erl \
    couch_query_servers.erl \
    couch_ref_counter.erl \
    couch_rep.erl \
    couch_rep_sup.erl \
    couch_server.erl \
    couch_server_sup.erl \
    couch_stats_aggregator.erl \
    couch_stats_collector.erl \
    couch_stream.erl \
    couch_task_status.erl \
    couch_util.erl \
    couch_view.erl \
    couch_view_compactor.erl \
    couch_view_updater.erl \
    couch_view_group.erl \
    couch_db_updater.erl

EXTRA_DIST = $(source_files) couch_db.hrl couch_stats.hrl

compiled_files = \
    couch.app \
    couch_btree.beam \
    couch_batch_save.beam \
    couch_batch_save_sup.beam \
    couch_config.beam \
    couch_config_writer.beam \
    couch_db.beam \
    couch_db_update_notifier.beam \
    couch_db_update_notifier_sup.beam \
    couch_doc.beam \
    couch_event_sup.beam \
    couch_external_manager.beam \
    couch_external_server.beam \
    couch_file.beam \
    couch_httpd.beam \
    couch_httpd_db.beam \
    couch_httpd_external.beam \
    couch_httpd_show.beam \
    couch_httpd_view.beam \
    couch_httpd_misc_handlers.beam \
    couch_httpd_stats_handlers.beam \
    couch_key_tree.beam \
    couch_log.beam \
    couch_os_process.beam \
    couch_query_servers.beam \
    couch_ref_counter.beam \
    couch_rep.beam \
    couch_rep_sup.beam \
    couch_server.beam \
    couch_server_sup.beam \
    couch_stats_aggregator.beam \
    couch_stats_collector.beam \
    couch_stream.beam \
    couch_task_status.beam \
    couch_util.beam \
    couch_view.beam \
    couch_view_compactor.beam \
    couch_view_updater.beam \
    couch_view_group.beam \
    couch_db_updater.beam

# doc_base = \
#     erlang.png \
#     index.html \
#     modules-frame.html \
#     overview-summary.html \
#     packages-frame.html \
#     stylesheet.css

# doc_modules = \
#     couch_btree.html \
#     couch_config.html \
#     couch_config_writer.html \
#     couch_db.html \
#     couch_db_update_notifier.html \
#     couch_db_update_notifier_sup.html \
#     couch_doc.html \
#     couch_event_sup.html \
#     couch_file.html \
#     couch_httpd.html \
#     couch_key_tree.html \
#     couch_log.html \
#     couch_query_servers.html \
#     couch_rep.html \
#     couch_rep_sup.html \
#     couch_server.html \
#     couch_server_sup.html \
#     couch_stream.html \
#     couch_util.html \
#     couch_view.html

couch.app: couch.app.tpl
	sed -e "s|%package_name%|@package_name@|g" \
	    -e "s|%version%|@version@|g" > \
	$@ < $<
	chmod +x $@

# $(dist_devdoc_DATA): edoc-info

# $(ERL) -noshell -run edoc_run files [\"$<\"]

%.beam: %.erl couch_db.hrl
	$(ERLC) $(ERLC_FLAGS) ${TEST} $<;

install-data-hook:
	if test -f "$(DESTDIR)$(couchprivlibdir)/couch_erl_driver"; then \
	    rm -f "$(DESTDIR)$(couchprivlibdir)/couch_erl_driver.so"; \
	    cd "$(DESTDIR)$(couchprivlibdir)" && \
	        $(LN_S) couch_erl_driver couch_erl_driver.so; \
	fi
if WINDOWS
# libtool and automake have defeated markh.  For each of our executables
# we end up with 2 copies - one directly in the 'target' folder (eg, 'priv')
# and another - the correct one - in .libs.  The former doesn't work but is 
# what gets installed for 'couchspawnkillable' - but the correct one for
# couchjs.exe *does* get copied.  *shrug*  So just clobber it with the 
# correct one here...
	$(INSTALL) priv/.libs/couchspawnkillable.exe "$(DESTDIR)$(couchprivdir)/."
endif

uninstall-local:
	if test -f "$(DESTDIR)$(couchprivlibdir)/couch_erl_driver"; then \
	    rm -f "$(DESTDIR)$(couchprivlibdir)/couch_erl_driver.so"; \
	fi
