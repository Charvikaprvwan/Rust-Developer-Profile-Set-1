# Rust-Developer-Profile-Set-1
  Question 1.Implement a function that checks whether a given string is a palindrome or not
  fn is_palindrome(s: &str) -> bool {
    let reversed = s.chars().rev().collect::<String>();
    s == reversed
}

fn main() {
    let test_string = "racecar";
    if is_palindrome(test_string) {
        println!("{} is a palindrome.", test_string);
    } else {
        println!("{} is not a palindrome.", test_string);
    }
}

Question 2.Given a sorted array of integers, implement a function that returns the index of the first occurrence of a given number.

fn find_first_occurrence(arr: &[i32], target: i32) -> Option<usize> {
    let mut left = 0;
    let mut right = arr.len() - 1;
    let mut result = None;

    while left <= right {
        let mid = left + (right - left) / 2;

        if arr[mid] == target {
            result = Some(mid);
            right = mid - 1; // Continue searching on the left side
        } else if arr[mid] < target {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }

    result
}

fn main() {
    let arr = [1, 2, 2, 2, 3, 4, 5];
    let target = 2;

    if let Some(index) = find_first_occurrence(&arr, target) {
        println!("The first occurrence of {} is at index {}", target, index);
    } else {
        println!("{} not found in the array.", target);
    }
}

  Question 3.Given a string of words, implement a function that returns the shortest word in the string.
   fn shortest_word(s: &str) -> Option<&str> {
    s.split_whitespace().min_by_key(|word| word.len())
}

fn main() {
    let sentence = "The quick brown fox jumps over the lazy dog";
    if let Some(shortest) = shortest_word(sentence) {
        println!("The shortest word is: {}", shortest);
    } else {
        println!("No words found in the input string.");
    }
}
Question 4.Implement a function that checks whether a given number is prime or not.
fn is_prime(n: u64) -> bool {
    if n <= 1 {
        return false;
    }
    if n <= 3 {
        return true;
    }
    if n % 2 == 0 || n % 3 == 0 {
        return false;
    }
    let mut i = 5;
    while i * i <= n {
        if n % i == 0 || n % (i + 2) == 0 {
            return false;
        }
        i += 6;
    }
    true
}

fn main() {
    let number = 29;
    if is_prime(number) {
        println!("{} is a prime number.", number);
    } else {
        println!("{} is not a prime number.", number);
    }
}

Question 5.Given a sorted array of integers, implement a function that returns the median of the array.
fn find_median(arr: &[i32]) -> f64 {
    let len = arr.len();
    if len % 2 == 0 {
        let mid_right = len / 2;
        let mid_left = mid_right - 1;
        (arr[mid_left] + arr[mid_right]) as f64 / 2.0
    } else {
        arr[len / 2] as f64
    }
}

fn main() {
    let arr_even = [1, 2, 3, 4, 5, 6];
    let arr_odd = [1, 2, 3, 4, 5];

    println!("Median of even-length array: {}", find_median(&arr_even));
    println!("Median of odd-length array: {}", find_median(&arr_odd));
}

Question6.Implement a function that finds the longest common prefix of a given set of strings.

fn longest_common_prefix(strings: &[&str]) -> String {
    if strings.is_empty() {
        return String::new();
    }

    let first_string = strings[0];
    let mut prefix = String::new();

    'outer: for (i, ch) in first_string.chars().enumerate() {
        for string in &strings[1..] {
            if let Some(c) = string.chars().nth(i) {
                if c != ch {
                    break 'outer;
                }
            } else {
                break 'outer;
            }
        }
        prefix.push(ch);
    }

    prefix
}

fn main() {
    let strings = ["flower", "flow", "flight"];
    println!("Longest common prefix: {}", longest_common_prefix(&strings));
}

Question 7.Implement a function that returns the kth smallest element in a given array.
fn kth_smallest(arr: &[i32], k: usize) -> Option<i32> {
    if k > arr.len() {
        return None;
    }

    let mut sorted_arr = arr.to_vec();
    sorted_arr.sort();

    Some(sorted_arr[k - 1])
}

fn main() {
    let arr = [3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5];
    let k = 5;
    if let Some(kth) = kth_smallest(&arr, k) {
        println!("The {}th smallest element is: {}", k, kth);
    } else {
        println!("Invalid input.");
    }
}

Question 8.Given a binary tree, implement a function that returns the maximum depth of the tree.
use std::cmp;

// Definition for a binary tree node.
#[derive(Debug)]
struct TreeNode {
    val: i32,
    left: Option<Box<TreeNode>>,
    right: Option<Box<TreeNode>>,
}

impl TreeNode {
    fn new(val: i32) -> Self {
        TreeNode { val, left: None, right: None }
    }
}

fn max_depth(root: Option<&Box<TreeNode>>) -> i32 {
    match root {
        Some(node) => {
            let left_depth = max_depth(node.left.as_ref());
            let right_depth = max_depth(node.right.as_ref());
            1 + cmp::max(left_depth, right_depth)
        },
        None => 0,
    }
}

fn main() {
    let mut root = TreeNode::new(1);
    let mut left = TreeNode::new(2);
    let mut right = TreeNode::new(3);
    let left_right = TreeNode::new(4);
    let left_left = TreeNode::new(5);

    left.right = Some(Box::new(left_right));
    left.left = Some(Box::new(left_left));

    root.left = Some(Box::new(left));
    root.right = Some(Box::new(right));

    println!("Maximum depth of the binary tree is: {}", max_depth(Some(&Box::new(root))));
}

Question 9.Reverse a string in Rust
fn reverse_string(s: &str) -> String {
    let mut reversed_chars: Vec<char> = s.chars().collect();
    reversed_chars.reverse();
    reversed_chars.into_iter().collect()
}

fn main() {
    let s = "Hello, world!";
    let reversed = reverse_string(s);
    println!("Original: {}", s);
    println!("Reversed: {}", reversed);
}

Question 10.Check if a number is prime in Rust.
fn is_prime(n: u64) -> bool {
    if n <= 1 {
        return false;
    }
    if n <= 3 {
        return true;
    }
    if n % 2 == 0 || n % 3 == 0 {
        return false;
    }
    let mut i = 5;
    while i * i <= n {
        if n % i == 0 || n % (i + 2) == 0 {
            return false;
        }
        i += 6;
    }
    true
}

fn main() {
    let number = 29;
    if is_prime(number) {
        println!("{} is a prime number.", number);
    } else {
        println!("{} is not a prime number.", number);
    }
}

Question 11.Merge two sorted arrays in Rust
fn merge_sorted_arrays(arr1: &[i32], arr2: &[i32]) -> Vec<i32> {
    let mut merged = Vec::new();
    let mut i = 0;
    let mut j = 0;

    while i < arr1.len() && j < arr2.len() {
        if arr1[i] < arr2[j] {
            merged.push(arr1[i]);
            i += 1;
        } else {
            merged.push(arr2[j]);
            j += 1;
        }
    }

    merged.extend_from_slice(&arr1[i..]);
    merged.extend_from_slice(&arr2[j..]);

    merged
}

fn main() {
    let arr1 = [1, 3, 5, 7];
    let arr2 = [2, 4, 6, 8, 10];
    let merged = merge_sorted_arrays(&arr1, &arr2);
    println!("{:?}", merged);
}

Question 12.Find the maximum subarray sum in Rust
fn max_subarray_sum(arr: &[i32]) -> i32 {
    let mut max_ending_here = 0;
    let mut max_so_far = std::i32::MIN;

    for &num in arr {
        max_ending_here = num.max(max_ending_here + num);
        max_so_far = max_so_far.max(max_ending_here);
    }

    max_so_far
}

fn main() {
    let arr = [-2, 1, -3, 4, -1, 2, 1, -5, 4];
    let max_sum = max_subarray_sum(&arr);
    println!("Maximum subarray sum is: {}", max_sum);
}
