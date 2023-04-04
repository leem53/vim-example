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

