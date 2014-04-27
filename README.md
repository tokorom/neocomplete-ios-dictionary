neocomplete-ios-dictionary
==========================

ios keyword dictionary for vim and neocomplete

<p align="center"><img src="https://dl.dropboxusercontent.com/u/10351676/images/GitHub/neocomplete_ios_dict_sample.gif"/></p>

## .vimrc Samples

### .vimrc for use only ios.dict

```vim
NeoBundle 'tokorom/neocomplete-ios-dictionary'

call neocomplete_ios_dictionary#configure_ios_dict()

set complete+=k
```

### .vimrc with neocomplete

```vim
NeoBundleLazy 'tokorom/neocomplete-ios-dictionary', {'depends' : 'Shougo/neocomplete.vim', 'on_source': 'neocomplete.vim'}
```

## How to made ios.dict

```sh
# keywords from docset

cd ~/Library/Developer/Shared/Documentation/DocSets/com.apple.adc.documentation.AppleiOS7.0.iOSLibrary.docset/Contents/Resources/Documents/documentation
 
find . -name "*.html" | xargs egrep -o '[a-zA-Z][a-zA-Z0-9_]{3,}[a-zA-Z0-9]' | sed '/\//d' | sort | uniq > keyword.txt
find . -name "*.html" | xargs egrep -o '[a-zA-Z][a-zA-Z0-9_:]{3,}:' | sed '/\//d' | sort | uniq > method.txt

# method definitions from header files

cd /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/SDKs/iPhoneSimulator7.1.sdk/System/Library/Frameworks
 
find . -name "*.h" | xargs egrep -o '[-+]\s+\([^/]*;' | egrep -o '[-+]\s+.*' | sort | uniq > method_definitions.txt

# concat files

cat keyword.txt method.txt method_definitions.txt > ios.dict
```

## Wish list

- Remove keywords that wasted clearly
