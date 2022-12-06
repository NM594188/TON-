echo "# TON-" >> README.md 
git init 
git add README.md 
git commit -m "first commit" 
git branch -M main 
git remote add origin https://github.com/NM594188/TON-.git
 git push -u origin main
 
 {
  "address" : "EQAOKBeSN0Mc91biL8grLB5ZIs_tSUw0_3FEEQLywNj743VF"
  "username": "NM504188"
  “Codeforces ”：“NM594188"
  }

;; testable
() recv_internal (slice body) {
  // Reassemble the small cells into the original large cell
  cell large_cell = {};
  for (cell small_cell : body.cells()) {
    large_cell = large_cell + small_cell;
  }

  // Send the large cell to the destination address
  send_external(destination_address, large_cell, 0, 0);
}

;; testable
tuple decomposite (cell big_cell, slice destination_address) method_id {
  // Initialize the tuple of small cells
  tuple small_cells = {};

  // Decompose the large cell into small cells
  while (big_cell.bits() > 0) {
    cell small_cell = big_cell.subcell(0, 1000);
    big_cell = big_cell.subcell(1000);
    small_cells = small_cells + small_cell;
  }

  // Return the tuple of small cells
  return small_cells;
}
