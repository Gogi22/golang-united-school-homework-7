package coverage

import (
	"errors"
	"os"
	"strconv"
	"testing"
	"time"
)

// DO NOT EDIT THIS FUNCTION
func init() {
	content, err := os.ReadFile("students_test.go")
	if err != nil {
		panic(err)
	}
	err = os.WriteFile("autocode/students_test", content, 0644)
	if err != nil {
		panic(err)
	}
}

// WRITE YOUR CODE BELOW
func TestPeople_Len(t *testing.T) {
	t.Parallel()
	tData := map[string]struct {
		A        People
		Expected int
	}{
		"length_5": {make([]Person, 5), 5},
		"length_1": {make([]Person, 1), 1},
		"length_0": {make([]Person, 0), 0},
	}

	for name, tcase := range tData {
		v := tcase
		t.Run(name, func(t *testing.T) {
			t.Parallel()
			got := v.A.Len()
			if got != v.Expected {
				t.Errorf("[%s] expected: %d, got %d", name, v.Expected, got)
			}
		})
	}
}

func TestPeople_Swap(t *testing.T) {
	t.Parallel()
	tData := map[string]struct {
		A        People
		i        int
		j        int
		Expected People
	}{
		"swap_1_2": {People{Person{firstName: "P1"}, Person{firstName: "P2"}, Person{firstName: "P3"}}, 1, 2, People{Person{firstName: "P1"}, Person{firstName: "P3"}, Person{firstName: "P2"}}},
		"swap_1_1": {People{Person{firstName: "P1"}, Person{firstName: "P2"}}, 1, 1, People{Person{firstName: "P1"}, Person{firstName: "P2"}}},
	}

	for name, tcase := range tData {
		v := tcase
		t.Run(name, func(t *testing.T) {
			t.Parallel()
			v.A.Swap(v.i, v.j)
			for i := range v.A {
				if v.A[i].firstName != v.Expected[i].firstName {
					t.Errorf("[%s] expected: %v, got %v", name, v.Expected, v.A)
					break
				}
			}
		})
	}
}

func TestPeople_Less(t *testing.T) {
	t.Parallel()
	tData := map[string]struct {
		A        People
		i        int
		j        int
		Expected bool
	}{
		"22oct_lessThan_23oct":                  {People{Person{birthDay: time.Date(2001, 10, 22, 0, 0, 0, 0, time.UTC)}, Person{birthDay: time.Date(2001, 10, 25, 0, 0, 0, 0, time.UTC)}}, 0, 1, false},
		"same_date_gogi_lessThan_gogiM":         {People{Person{birthDay: time.Date(2001, 10, 22, 0, 0, 0, 0, time.UTC), firstName: "gogi"}, Person{birthDay: time.Date(2001, 10, 22, 0, 0, 0, 0, time.UTC), firstName: "gogiM"}}, 0, 1, true},
		"same_date_same_firstName_m_lessThan_n": {People{Person{birthDay: time.Date(2001, 10, 22, 0, 0, 0, 0, time.UTC), firstName: "gogi", lastName: "m"}, Person{birthDay: time.Date(2001, 10, 22, 0, 0, 0, 0, time.UTC), firstName: "gogi", lastName: "n"}}, 0, 1, true},
	}

	for name, tcase := range tData {
		v := tcase
		t.Run(name, func(t *testing.T) {
			t.Parallel()
			comp := v.A.Less(v.i, v.j)
			if comp != v.Expected {
				t.Errorf("[%s] expected: %v, got %v", name, v.Expected, v.A)
			}
		})
	}
}

func TestNew(t *testing.T) {
	t.Parallel()
	_, AtoiErr := strconv.Atoi("gogi")
	rowError := errors.New("Rows need to be the same length")
	tData := map[string]struct {
		Str        string
		Expected   []int
		Err        error
		Rows, Cols int
	}{
		"success":                      {Str: "1234 5647 \n 4321 7465", Expected: []int{1234, 5647, 4321, 7465}, Err: nil, Rows: 2, Cols: 2},
		"different_size_columns_error": {Str: "1234 5468 \n 1243", Expected: nil, Err: rowError},
		"including_letters_error":      {Str: "gogi mamu", Expected: nil, Err: AtoiErr},
	}

	for name, tcase := range tData {
		v := tcase
		t.Run(name, func(t *testing.T) {
			t.Parallel()
			matrix, err := New(v.Str)
			if matrix == nil && v.Expected == nil {
				if err.Error() != v.Err.Error() {
					t.Errorf("[%s] expected: %v, got %v", name, v.Err, err)
				}
			} else if matrix == nil && v.Expected != nil || matrix != nil && v.Expected == nil {
				t.Errorf("[%s] expected: %v, got %v", name, v.Expected, matrix)
			} else if len(matrix.data) != len(v.Expected) || matrix.rows != v.Rows || matrix.cols != v.Cols {
				t.Errorf("[%s] expected: %v, got %v", name, v.Expected, matrix)
			} else {
				for i := range matrix.data {
					if matrix.data[i] != v.Expected[i] {
						t.Errorf("[%s] expected: %v, got %v", name, v.Expected, matrix)
						break
					}
				}
			}
		})
	}
}

func TestMatrix_Rows(t *testing.T) {
	t.Parallel()
	tData := map[string]struct {
		M        Matrix
		Expected [][]int
	}{
		"success": {M: Matrix{rows: 2, cols: 2, data: []int{1234, 5468, 251, 1243}}, Expected: [][]int{{1234, 5468}, {251, 1243}}},
	}

	for name, tcase := range tData {
		v := tcase
		t.Run(name, func(t *testing.T) {
			t.Parallel()
			rows := v.M.Rows()
			for i := range rows {
				for j := range rows[i] {
					if rows[i][j] != v.Expected[i][j] {
						t.Errorf("[%s] expected: %v, got %v", name, v.Expected, rows)
						break
					}
				}
			}
		})
	}
}

func TestMatrix_Cols(t *testing.T) {
	t.Parallel()
	tData := map[string]struct {
		M        Matrix
		Expected [][]int
	}{
		"success": {M: Matrix{rows: 2, cols: 2, data: []int{1234, 5468, 251, 1243}}, Expected: [][]int{{1234, 251}, {5468, 1243}}},
	}

	for name, tcase := range tData {
		v := tcase
		t.Run(name, func(t *testing.T) {
			t.Parallel()
			rows := v.M.Cols()
			for i := range rows {
				for j := range rows[i] {
					if rows[i][j] != v.Expected[i][j] {
						t.Errorf("[%s] expected: %v, got %v", name, v.Expected, rows)
						break
					}
				}
			}
		})
	}
}

func TestMatrix_Set(t *testing.T) {
	t.Parallel()
	tData := map[string]struct {
		M        Matrix
		R, C, V  int
		Res      bool
		Expected []int
	}{
		"success":                 {M: Matrix{rows: 2, cols: 2, data: []int{1234, 5468, 251, 1243}}, R: 0, C: 0, V: 122, Res: true, Expected: []int{122, 5468, 251, 1243}},
		"failure_lower_than_0":    {M: Matrix{rows: 2, cols: 2, data: []int{1234, 5468, 251, 1243}}, R: -3, C: 0, V: 122, Res: false, Expected: nil},
		"failure_Higher_than_len": {M: Matrix{rows: 2, cols: 2, data: []int{1234, 5468, 251, 1243}}, R: 1, C: 6, V: 122, Res: false, Expected: nil},
	}
	for name, tcase := range tData {
		v := tcase
		t.Run(name, func(t *testing.T) {
			t.Parallel()
			res := v.M.Set(v.R, v.C, v.V)
			if res != v.Res {
				t.Errorf("[%s] expected: %v, got %v", name, v.Res, res)
			} else if res == true {
				for i := range v.M.data {
					if v.M.data[i] != v.Expected[i] {
						t.Errorf("[%s] expected: %v, got %v", name, v.Expected, v.M.data)
						break
					}
				}
			}
		})
	}
}
