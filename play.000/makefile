flex-cssfiles := css/flex.browser.css css/flex.debug.css

web-flex-cssfiles := $(flex-cssfiles)
web-flex-allfiles := html/flex.html $(web-flex-cssfiles)
web-flex-binfiles := bin/web-flex-browser/flex.html $(subst .browser,,$(subst css/,bin/web-flex-browser/,$(flex-cssfiles)))

web-files := dir/graph_editor.ext dir/graph_diagram.ext
web-htmlfiles := $(subst dir,html,$(subst .ext,.html,$(web-files)))
web-cssfiles := $(subst dir,css,$(subst .ext,.css,$(web-files))) css/main.css css/main.debug.css
web-jsfiles := $(subst dir,js,$(subst .ext,.js,$(web-files)))
web-genfiles := $(subst dir,css,$(subst .ext,.css,$(web-files))) $(subst dir,js,$(subst .ext,.js,$(web-files)))
web-otherfiles := $(web-cssfiles) $(web-jsfiles)
web-allfiles := $(web-htmlfiles) $(web-otherfiles)
web-binfiles := $(subst html/,bin/web-browser/,$(web-htmlfiles)) $(subst css/,bin/web-browser/,$(web-cssfiles)) $(subst js/,bin/web-browser/,$(web-jsfiles))

flex-web-binfiles := $(subst .browser,,$(subst css/,bin/web-browser/,$(flex-cssfiles)))

all: web

web-ensure-files:
	for f in $(web-otherfiles); do [ -f $$f ] || touch $$f; done

web-flex: web-flex-chrome web-flex-firefox

web-flex-chrome:
	[ -d bin/web-flex-chrome ] || mkdir -p bin/web-flex-chrome
	cp -f $(subst browser,chrome,$(web-flex-allfiles)) bin/web-flex-chrome
	mv bin/web-flex-chrome/flex.chrome.css bin/web-flex-chrome/flex.css

web-flex-firefox:
	[ -d bin/web-flex-firefox ] || mkdir -p bin/web-flex-firefox
	cp -f $(subst browser,firefox,$(web-flex-allfiles)) bin/web-flex-firefox
	mv bin/web-flex-firefox/flex.firefox.css bin/web-flex-firefox/flex.css

web: web-chrome web-firefox

web-chrome: web-ensure-files $(web-allfiles)
	[ -d bin/web-chrome ] || mkdir -p bin/web-chrome
	cp -f  $(subst browser,chrome,$(web-allfiles))  $(subst browser,chrome,$(web-flex-cssfiles)) bin/web-chrome
	mv bin/web-chrome/flex.chrome.css bin/web-chrome/flex.css

web-firefox: web-ensure-files $(web-allfiles)
	[ -d bin/web-firefox ] || mkdir -p bin/web-firefox
	cp -f  $(subst browser,firefox,$(web-allfiles))  $(subst browser,firefox,$(web-flex-cssfiles)) bin/web-firefox
	mv bin/web-firefox/flex.firefox.css bin/web-firefox/flex.css

clean: web-flex-chrome-clean web-chrome-clean web-flex-firefox-clean web-firefox-clean

web-flex-chrome-clean:
	-rm  $(subst browser,chrome,$(web-flex-binfiles))
	-rmdir bin/web-flex-chrome

web-chrome-clean:
	-rm  $(subst browser,chrome,$(web-binfiles))  $(subst browser,chrome,$(flex-web-binfiles))
	-rmdir bin/web-chrome
	for f in $(web-genfiles); do [ -f "$$f" ] && ! [ -s "$$f" ] && rm $$f; done

web-flex-firefox-clean:
	-rm  $(subst browser,firefox,$(web-flex-binfiles))
	-rmdir bin/web-flex-firefox

web-firefox-clean:
	-rm  $(subst browser,firefox,$(web-binfiles))  $(subst browser,firefox,$(flex-web-binfiles))
	-rmdir bin/web-firefox
	for f in $(web-genfiles); do [ -f "$$f" ] && ! [ -s "$$f" ] && rm $$f; done