# Rust implement matrix

```rust
/**
 * implment matrix function
*/
#[allow(dead_code)]
#[allow(unused_variables)]
#[allow(unused_mut)]
#[allow(non_snake_case)]
pub mod matrix {
    pub fn new(m:usize,n:usize) -> Vec<Vec<f64>>{ //返回0组成的n*m矩阵 vec
        let mut mat = Vec::new();
        for i in 0..m {
            mat.push(vec![0; n].iter().map(|s| *s as f64).collect::<Vec<_>>());
        }
        let vec = mat.clone();
        vec
    }
    pub fn find_frist(matrix:&Vec<Vec<f64>>,target:i32)->(usize,usize) {
        let mut m:usize = 0;
        let mut n:usize = 0;
        for (index_i, item_i) in matrix.iter().enumerate() {
            for (index_j, item_j) in item_i.iter().enumerate() {
                if *item_j == target as f64{
                    m = index_j;
                    n = index_i;
                    break;
                }
            }
        }
        (n,m)
    }
    pub fn is_square_matrix(matrix:&Vec<Vec<f64>>)->bool {
        let m = &matrix.len();
        let n = &matrix[0].len();
        if n == m {
            return true;
        }else{
            return false;
        }
    }
    /**方阵类型
    上三角矩阵,Upper triangular matrix  上三角矩阵（Upper Triangular Matrix）是指主对角线以下元素全为0的矩阵
    下三角矩阵,lower triangular matrix  下三角矩阵（Lower Triangular Matrix）是指主对角线以上元素全为0的矩阵
    对角矩阵,diagonal matrix  对角矩阵（Diagonal Matrix）是指除主对角线之外其他元素都为0的矩阵
    单位矩阵,identity matrix
    对称矩阵,Symmetric Matrix    对称矩阵（Symmetric Matrix）是指元素以主对角线为对称轴对应相等的矩阵
    **/
    pub fn square_matrix_type(matrix:&Vec<Vec<f64>>)->String{
       
        if !is_square_matrix(&matrix) {
            return "Is not square matrix".into();
        }

        //is upper triangular matrix
        fn is_upper_triangular_matrix(matrix:&Vec<Vec<f64>>) -> String {
            let mut is_upper_triangular = true;
            for (index_i, item_i) in matrix.iter().enumerate() {
                for (index_j, item_j) in item_i.iter().enumerate() {
                    if index_j > index_i{
                        if *item_j!=0.0{
                            is_upper_triangular = false;
                        }
                    }
                }
            }
            let mut result = "".into();
            if is_upper_triangular{
                result="Upper".into();
            }
            result
        }

        //is lowwer triangular matrix
        fn is_lower_triangular_matrix(matrix: &Vec<Vec<f64>>)->String{
            let mut is_lower_triangular = true;
            for (index_i, item_i) in matrix.iter().enumerate() {
                for (index_j, item_j) in item_i.iter().enumerate() {
                    if index_j < index_i{
                        if *item_j!=0.0{
                            is_lower_triangular = false;
                        }
                    }
                }
            }
            let mut result = "".into();
            if is_lower_triangular{
                result= "Lower".into();
            }
            result
        }

        //is diagonal triangular matrix
        fn is_diagonal_triangular_matrix(matrix: &Vec<Vec<f64>>)->String{
            let mut is_diagonal_triangular = true;
            for (index_i, item_i) in matrix.iter().enumerate() {
                for (index_j, item_j) in item_i.iter().enumerate() {
                    if index_j > index_i{
                        if *item_j!=0.0{
                            is_diagonal_triangular = false;
                        }
                    }
                    if index_j < index_i{
                        if *item_j!=0.0{
                            is_diagonal_triangular = false;
                        }
                    }
                }
            }
            let mut result = "".into();
            if is_diagonal_triangular{
                result="Diagonal".into();
            }
            result
        }


        //is Symmetric triangular matrix
        fn is_symmetric_triangular(matrix:&Vec<Vec<f64>>)->String{
            let mut is_Symmetric_triangular = true;
            let mut not_diagonal:Vec<i32> = vec![];
            for (index_i, item_i) in matrix.iter().enumerate() {
                for (index_j, item_j) in item_i.iter().enumerate() {
                    if matrix[index_i][index_j]==matrix[index_j][index_i] && index_i!=index_j{
                        not_diagonal.push(1);
                    }
                }
            }
       

            let Not_diagonal = not_diagonal.len();
            let m = &matrix.len();
            let n = &matrix[0].len();
            let mut expected_Not_diagonal = m*n-n;
            let mut result = "".into();
            // println!("{:?}  {:?} {:?}",Not_diagonal==expected_Not_diagonal,Not_diagonal,expected_Not_diagonal);
            if Not_diagonal==expected_Not_diagonal{
                result= "Symmetric".into();
            }
            return result;
        }

        //identity matrix
        fn is_identity_matrix(matrix:&Vec<Vec<f64>>)->String{
            let mut result = "".to_owned();
            if is_diagonal_triangular_matrix(&matrix)=="Diagonal".to_string(){
                  for (index_i, item_i) in matrix.iter().enumerate() {
                    for (index_j, item_j) in item_i.iter().enumerate() {
                        if index_j == index_i && matrix[index_j][index_i] ==1.0 {
                            result = "identity".to_owned();
                        }
                    }
                  }
            }
            result
        }

        let mut result = vec![];
        result.push(is_upper_triangular_matrix(&matrix));
        result.push(is_lower_triangular_matrix(&matrix));
        result.push(is_diagonal_triangular_matrix(&matrix));
        result.push(is_symmetric_triangular(&matrix));
        result.push(is_identity_matrix(&matrix).to_string());
        // println!("{:?}",result);
        return result.iter().filter(|s| !s.is_empty()).map(|s| s.to_owned()).collect();

        
    }
    pub fn multiply_matrix<'a>(matrix1:&'a Vec<Vec<f64>>,matrix2:&'a Vec<Vec<f64>>)->Vec<Vec<f64>>{
        let m = &matrix2.len();
        let n = &matrix1[0].len();
        let mut matrix3:Vec<Vec<f64>> = new(*&matrix2.len(),*&matrix2[0].len());    //创建0组成的m*n 矩阵
        // println!("{:?}",&matrix3);
        for i in 0..*&matrix2.len(){    
            for j in 0..*&matrix2[0].len(){    
                for k in 0..*m{    
                    matrix3[i][j] += matrix1[i][k] * matrix2[k][j];    
                }    
            }    
        }    
        matrix3 //返回两个矩阵的乘积
    }
    pub fn add_square_matrix<'a>(matrix1:&'a Vec<Vec<f64>>,matrix2:&'a Vec<Vec<f64>>)->Vec<Vec<f64>>{
        let mut matrix3 = matrix1.clone();
        for i in 0..*&matrix2.len(){
            for j in 0..*&matrix2.len(){
                matrix3[i][j] += matrix2[i][j];
            }
        }
        matrix3
    }
    //相减 矩阵
    pub fn sub_square_matrix<'a>(matrix1:&'a Vec<Vec<f64>>,matrix2:&'a Vec<Vec<f64>>)->Vec<Vec<f64>>{
        let mut matrix3 = matrix1.clone();
         for i in 0..*&matrix2.len(){
            for j in 0..*&matrix2.len(){
                matrix3[i][j] -= matrix2[i][j];
            }
        }
        matrix3
    }

    //is matrix the same（相等矩阵）
    pub fn matrix_is_same<'a>(matrix1:&'a Vec<Vec<f64>>,matrix2:&'a Vec<Vec<f64>>)->bool{
        let mut is_the_same = true;
        for i in 0..*&matrix2.len(){
            for j in 0..*&matrix2[0].len(){
                if matrix2[i][j]!=matrix1[i][j]{
                    is_the_same= false;
                }
            }
        }
        is_the_same
    }
    //返回 矩阵的转置
    pub fn matrix_transpose<'a>(matrix:&'a Vec<Vec<f64>>)->Vec<Vec<f64>>{
        let mut matrix1 = matrix.clone();
        for i in 0..*&matrix.len(){
            for j in 0..*&matrix[0].len(){
                matrix1[i][j]=matrix[j][i];
            }
        }
        matrix1
    }
    //矩阵A为n阶方阵，若存在n阶矩阵B，使得矩阵A、B的乘积为单位阵，则称A为可逆阵，B为A的逆矩阵
    pub fn is_invertible_matrix<'a>(matrix:&'a Vec<Vec<f64>>)->bool{
        fn getCofactor(mat:&mut Vec<Vec<f64>>, temp:&mut Vec<Vec<f64>>, p:usize, q:usize, n:usize){
            let mut i = 0;
            let mut j = 0;
            for row in 0..n{
                for col in 0..n{
                    if row != p && col != q{
                        temp[i][j] = mat[row][col];
                        j += 1;
                        if j == n - 1{
                            j = 0;
                            i += 1;
                        }
                    }
                }
            }
        }
        use std::sync::Arc;
        fn determinantOfMatrix(mat:&mut Vec<Vec<f64>>, n:usize)->f64{
            let mut D = 0.0;
            if n == 1{
                return mat[0][0];
            }
            let mut temp = Arc::new(new(n,n));
            let mut sign = 1.0;
            for f in 0..n{
                getCofactor(mat, &mut *Arc::get_mut(&mut temp).unwrap(), 0, f, n);
                D += sign * mat[0][f] *determinantOfMatrix(&mut *Arc::get_mut(&mut temp).unwrap(), n - 1);
                sign = -sign;
                }
        return D;
        }
        fn isInvertible(mat:&mut Vec<Vec<f64>>, n:usize)->bool{
            if determinantOfMatrix(mat, n) != 0.0{
                return true;
            }
            else{
            return false;
            }
        }
        let mut matrix1 = matrix.clone();
        let n = matrix.len();
        isInvertible(&mut matrix1,n)
    }
    //返回矩阵的伴随矩阵
    pub fn adjoin_matrix<'a>(matrix:&'a Vec<Vec<f64>>)->Vec<Vec<f64>>{
        let mut matrix1 = matrix.clone();
        matrix1

    }

    use std::sync::Arc;
    pub fn run(){
        let a_44 = new(2,2); //初始化一个m*n的矩阵 4*4 因为元素全是零 叫做零矩阵
        // println!("{:?},{}",&a_44,is_square_matrix(&a_44)); 
        let m1:Vec<Vec<f64>> = vec![
                    vec![1.0,2.0],
                    vec![1.0,2.0],
                    ];
        let m2:Vec<Vec<f64>> = vec![
                    vec![0.0,0.0],
                    vec![0.0,0.5],
                    ];
        let target_index = find_frist(&m1,50);

        // println!("M_{{{} {}}}",target_index.0, target_index.1); 
        // println!("taget:{}",&M[target_index.0][target_index.1]);
        let matrix_type = square_matrix_type(&*Arc::new(&m1));
        // println!("matrix_type:{}",matrix_type);

        // let mul_result = multiply_matrix(&m1,&m2);
        let mul_result = multiply_matrix(&m2,&m1);
        // println!("mul_result:{:?}",mul_result);

        let add_result = add_square_matrix(&m1,&m2);
        // println!("add_result:{:?}",add_result);
        
        let sub_result = sub_square_matrix(&m1,&m2);
        // println!("sub_result:{:?}",sub_result);

        let is_same = matrix_is_same(&m1,&m2);
        // println!("is_same:{:?}",is_same);

        let transpose_result = matrix_transpose(&m1);
        // println!("transpose_result:{:?}",transpose_result);

        let m3:Vec<Vec<f64>> = vec![
                    vec![1.0,3.0,5.0],
                    vec![1.0,5.0,5.0],
                    vec![3.0,2.0,5.0],
                    ];
        let adjoin_matrix = adjoin_matrix(&m3);
        // println!("adjoin_matrix:{:?}",adjoin_matrix);

        let is_invertible_matrix = is_invertible_matrix(&m3);
        println!("矩阵是否可逆  is_invertible:{:?}",is_invertible_matrix);

  
    }

}

```

