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
