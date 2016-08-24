flex-cssfiles := css/flex.css css/flex.debug.css

web-flex-htmlfiles := html/flex.html
web-flex-cssfiles := $(flex-cssfiles)
web-flex-allfiles := html/flex.html css/flex.css css/flex.debug.css
web-flex-binfiles := bin/web-flex/flex.html $(subst css/,bin/web-flex/,$(flex-cssfiles))

web-files := dir/graph_editor.ext dir/graph_diagram.ext
web-htmlfiles := $(subst dir,html,$(subst .ext,.html,$(web-files)))
web-cssfiles := $(subst dir,css,$(subst .ext,.css,$(web-files)))
web-jsfiles := $(subst dir,js,$(subst .ext,.js,$(web-files)))
web-otherfiles := $(web-cssfiles) $(web-jsfiles)
web-allfiles := $(web-htmlfiles) $(web-otherfiles)
web-binfiles := $(subst dir,bin/web,$(subst .ext,.html,$(web-files)) $(subst .ext,.css,$(web-files)) $(subst .ext,.js,$(web-files)))

flex-web-binfiles := $(subst css/,bin/web/,$(flex-cssfiles))

web-flex:
	[ -d bin/web-flex ] || mkdir -p bin/web-flex
	cp -f $(web-flex-allfiles) bin/web-flex

web-flex-clean:
	-rm $(web-flex-binfiles)
	-rmdir bin/web-flex

web: web-ensure-files $(web-allfiles)
	[ -d bin/web ] || mkdir -p bin/web
	cp -f $(web-allfiles)  $(web-flex-cssfiles) bin/web

web-ensure-files:
	for f in $(web-otherfiles); do [ -f $$f ] || touch $$f; done

web-clean:
	-rm $(web-binfiles) $(flex-web-binfiles)
	-rmdir bin/web
	for f in $(web-otherfiles); do [ -f "$1" ] && ! [ -s "$1" ] && rm $$f; done

clean: web-flex-clean web-clean