# chat-gpt-code-comment-challenge

First I prompted ChatGPT-4 for javascript to solve an easy to verify problem.  I asked it to not comment the code.

Model: GPT-4

Christopher Roge
you are a expert javascript programmer with more than 20 years experience.  You love writing efficient code.  You never add comments to your code because your code is so good it speaks for itself.  Your task is to write excellent code to solve the problem presented in the prompt.  Do you understand and do you have any questions?
Yes, I understand that I am an expert JavaScript programmer with over 20 years of experience and that I should write efficient and self-explanatory code to solve a given problem. However, I'd like to note that adding comments is generally considered a best practice in programming, as it helps others understand the code more easily.

Please provide me with the problem or task you would like me to solve using JavaScript.




Christopher Roge
I need a javascript function that will accept two arrays of CIDR notations and will return true if all of the addresses in the 2nd array would be included in the first array.  Be sure to include no code comments because your code is so good that it speaks for itself.
Here's the function you requested:

javascript
Copy code
function areSubnetsIncluded(cidrArray1, cidrArray2) {
  function parseCIDR(cidr) {
    const [address, mask] = cidr.split('/');
    const maskBits = -1 << (32 - +mask);
    const ipInt = address.split('.').reduce((acc, octet) => (acc << 8) + +octet, 0);
    return [ipInt & maskBits, maskBits];
  }

  function isSubnetIncluded(cidr1, cidr2) {
    const [subnet1, mask1] = parseCIDR(cidr1);
    const [subnet2, mask2] = parseCIDR(cidr2);
    return mask1 <= mask2 && (subnet1 & mask1) === (subnet2 & mask1);
  }

  return cidrArray2.every(cidr2 => cidrArray1.some(cidr1 => isSubnetIncluded(cidr1, cidr2)));
}
This function takes two arrays of CIDR notations and returns true if all addresses in the second array are included in the first array.
