# Quad_b_tech_interview
#Pranay Gupta

1. use std::io;

fn is_palindrome(s: &str) -> bool {
    let s_chars: Vec<char> = s.chars().collect();
    let reversed_chars: Vec<char> = s_chars.iter().rev().copied().collect();
    s_chars == reversed_chars
}
fn main() {
    println!("Enter a word to check if it's a palindrome:");
    let mut input = String::new();
    io::stdin().read_line(&mut input).expect("Failed to read input");
    input = input.trim().to_string();
    if is_palindrome(&input) {
        println!("Palindrome!");
    } else {
        println!("Not a palindrome.");
    }
}


2. fn first_occurrence(arr: &[i32], target: i32) -> Option<usize> {
    // Use binary search to find the index of the target
    match arr.binary_search(&target) {
        Ok(index) => {
            let first_occurrence = arr[..index].iter().rev().position(|&x| x != target).map(|pos| index - pos - 1).unwrap_or(index);
            Some(first_occurrence)
        }
        Err(_) => None, // Target not found
    }
}

fn main() {
    let sorted_array = vec![1, 2, 3, 3, 4, 5, 5, 5, 6];
    let target_number = 3;
    if let Some(index) = find_first_occurrence(&sorted_array, target_number) {
        println!("First occurrence of {} is at index {}", target_number, index);
    } else {
        println!("{} not found in the array.", target_number);
    }
}


3.  fn find_shortest_word(input: &str) -> Option<&str> {
    
    let words: Vec<&str> = input.split_whitespace().collect();

    
    let mut shortest_word: Option<&str> = None;
    let mut shortest_length = usize::MAX;

    for word in words {
        let word_length = word.len();
        if word_length < shortest_length {
            shortest_length = word_length;
            shortest_word = Some(word);
        }
    }

    shortest_word
}

fn main() {
    let input_string = "The dog was running in the garden.";
    if let Some(shortest) = find_shortest_word(input_string) {
        println!("The shortest word is: {}", shortest);
    } else {
        println!("No words found in the input string.");
    }
}



4. fn is_prime(n: u32) -> bool {
    if n <= 1 {
        return false;
    }


    let limit = (n as f64).sqrt() as u32;
    for i in 2..=limit {
        if n % i == 0 {
            return false;
        }
    }

    true
}

fn main() {
    let num = 11;
    if is_prime(num) {
        println!("{} is a prime number.", num);
    } else {
        println!("{} is not a prime number.", num);
    }
}



5. fn median(arr: &[i32]) -> f64 {
    let len = arr.len();
    let mid = len / 2;

    if len % 2 == 0 {
        let middle_sum = arr[mid - 1] + arr[mid];
        middle_sum as f64 / 2.0
    } else {
        arr[mid] as f64
    }
}

fn main() {
    let sorted_array = vec![1, 2, 3, 4, 5, 6, 7, 8, 9];
    let median_value = median(&sorted_array);
    println!("Median of the array: {}", median_value);
}


6. fn longest_common_prefix(strings: &[&str]) -> String {
    if strings.is_empty() {
        return String::new();
    }

    let (first, last) = (strings[0], strings.last().unwrap());

    let common_len = first
        .chars()
        .zip(last.chars())
        .take_while(|(a, b)| a == b)
        .count();

    first[..common_len].to_string()
}

fn main() {
    let strings = vec!["needforspeed", "need", "for", "speed"];
    println!("The longest common prefix is: {}", longest_common_prefix(&strings));
}


7. use std::collections::BinaryHeap;

fn kth_smallest(arr: &[i32], k: usize) -> Option<i32> {
    if k > arr.len() {
        return None;
    }
    let mut min_heap = BinaryHeap::with_capacity(k);
    for &num in arr {
        if min_heap.len() < k {
            min_heap.push(num);
        } else if let Some(&top) = min_heap.peek() {
            if num < top {
                min_heap.pop();
                min_heap.push(num);
            }
        }
    }
    min_heap.pop()
}
fn main() {
    let arr = vec![7, 10, 4, 3, 20, 15];
    let k = 3;
    match kth_smallest(&arr, k) {
        Some(val) => println!("The {}th smallest element is: {}", k, val),
        None => println!("Invalid value of k."),
    }
}


8.// Definition for a binary tree node.
#[derive(Debug, PartialEq, Eq)]
struct TreeNode {
    val: i32,
    left: Option<Box<TreeNode>>,
    right: Option<Box<TreeNode>>,
}

impl TreeNode {
    fn new(val: i32) -> Self {
        TreeNode {
            val,
            left: None,
            right: None,
        }
    }
}

fn max_depth(root: Option<Box<TreeNode>>) -> i32 {
    match root {
        Some(node) => {
            let left_depth = max_depth(node.left);
            let right_depth = max_depth(node.right);
            1 + std::cmp::max(left_depth, right_depth)
        }
        None => 0,
    }
}

fn main() {
    // Example usage:
    let mut root = TreeNode::new(3);
    root.left = Some(Box::new(TreeNode::new(9)));
    root.right = Some(Box::new(TreeNode::new(20)));
    root.right.as_mut().unwrap().left = Some(Box::new(TreeNode::new(15)));
    root.right.as_mut().unwrap().right = Some(Box::new(TreeNode::new(7)));
    println!("Maximum depth of the tree: {}", max_depth(Some(Box::new(root))));
}


9. fn reverse(s: &str) -> String {
    s.chars().rev().collect()
}

fn main() {
    let original = "hello";
    let reversed = reverse(original);
    println!("{} reversed is {}", original, reversed);
}


10.fn check_prime(num: i32, i: i32) -> bool {
    if i == 1 {
        return true;
    } else {
        if num % i == 0 {
            return false;
        } else {
            return check_prime(num, i - 1);
        }
    }
}

fn main() {
    let num = 11;
    let result = check_prime(num, num / 2);
    if result {
        println!("{} is a prime number.", num);
    } else {
        println!("{} is not a prime number.", num);
    }
}


11.fn merge_sorted_arrays(nums1: &[i32], nums2: &[i32]) -> Vec<i32> {
    let mut merged = nums1.to_vec();
    merged.extend_from_slice(nums2);
    merged.sort();
    merged
}

fn main() {
    let nums1 = vec![1, 3, 5, 7];
    let nums2 = vec![2, 4, 6, 8];
    let merged = merge_sorted_arrays(&nums1, &nums2);
    println!("Merged array: {:?}", merged);
}


12.fn max_subarray_sum(arr: Vec<i32>) -> i32 {
    let mut max_ending_here = arr[0];
    let mut max_so_far = arr[0];
    for &num in &arr[1..] {
        max_ending_here = num.max(max_ending_here + num);
        max_so_far = max_so_far.max(max_ending_here);
    }
    max_so_far
}

fn main() {
    let arr = vec![-2, -3, 4, -1, -2, 1, 5, -3];
    let max_sum = max_subarray_sum(arr);
    println!("Maximum subarray sum: {}", max_sum);
}

