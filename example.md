Jump to @ sign, this is your vim-refactoring starting point.

## Example 1

@
Rename "width" to "length"

´´´
  METHOD get_text.
    result = |Invalid width.|.
  ENDMETHOD.
´´´

5j      "5 lines down"
fw      "forward to first occurence of w"
cw      "change word"
length  "enter text"

## Example 2

@
Correct typing error "ont" to "not"

´´´
  METHOD get_text.
    result = |File could ont be read.|.
  ENDMETHOD.
´´´

/ont<cr>  "search for 'ont'"
n         "next occurence"
x         "delete character"
p         "paste content of buffer (o) after cursor"

## Example 3

@
Remove prefixes of parameters

´´´
  METHODS:
    process
      IMPORTING
        i_text_before       TYPE string
        i_width             TYPE i
      RETURNING
        VALUE(r_text_after) TYPE stringtab.
´´´

/i_<cr>   "search for 'i_'; this will jump to the beginning of i_text_before"
ctrl+2, r "rename in file; this will rename all occurences of i_text_before"
2x        "remove character under cursor and next one"
<cr>      "end renaming"
n         "find next occurence of last searched string ('i_'); this will jump to the beginning of i_width"
ctrl+2, r "rename in file; this will rename all occurences of i_width"
2x        "remove character under cursor and next one"
<cr>      "end renaming"
2j        "2 lines down"
fr        "forward to first occurence of r"
ctrl+2, r "rename in file; this will rename all occurences of r_text_after"
2x        "remove character under cursor and next one"
<cr>      "end renaming"
