# 8.BAA-Bits
Listing 8 BAA-Bits/Bits.java Page 26

### 5.1.4 Bit-wise operators

We can operate on variables of integral types (mainly `int`) treating them as “buckets” of single bits. In what follows, remember that operations of shifting, ANDing, ORing etc., that we discuss, do not modify their arguments: they return new values that we have to handle in some way (display, assign to a variables, and so on).

As we know, data in a variable is stored as a sequence of bits, conventionally represented by 0 and 1. In particular an int consists of 32 bits. We can interpret individual bits as coefficients at powers of 2: the rightmost (least significant) bit is the coefficient at 2<sup>0</sup>, the next, from the right, at 2<sup>1</sup>, the next at 2<sup>2</sup> and so on, to the last (i.e., the leftmost, most significant) bit which stands at 231.

### Shifting
Shift operators act on values of integral types: they yield another value, which corresponds to the original one but with all bits shifted by a specified number of positions to the left or to the right.

Left shift (`<<`) moves the bit pattern to the left: bits on the left which go out of the variable are lost, bits which enter from the right are all 0. The value to be shifted is given as the left-hand operand while number of positions to shift – by the right-hand operand. For example (we use only eight bits to simplify notation, in reality there are 32 bits in an `int`):

```
a          1 0 1 0 0 1 1 0
a << 3     0 0 1 1 0 0 0 0
```

The _unsigned_ right shift operator (`>>>`) does the same but in the opposite direction

```
a          1 0 1 0 0 1 1 0
a >>> 3    0 0 0 1 0 1 0 0
```

The _signed_ right shift operator (`>>`) behaves in a similar way, but what comes in from the left is the sign bit: if the leftmost bit is 0, zeros will come in, if it is 1, these will be ones

```
a          1 0 1 0 0 1 1 0
a >> 3     1 1 1 1 0 1 0 0
b          0 0 1 0 0 1 1 0
b >> 3     0 0 0 0 0 1 0 0
```

### ANDing, ORing, etc.
Bit-wise operations work similarly to logical ones (ANDing, ORing, XORing, negating) but operate on individual bits of their operands which must be of an integral type.

For example, when ANDing two values with bit-wise AND operator (`&`) we will get a new value, where on each position there is 1 if and only if in both operands there were 1s on this position, and 0 otherwise

```
a          1 0 1 0 0 1 0 0
b          1 0 0 0 0 1 1 0
a & b      1 0 0 0 0 1 0 0
```

For bit-wise OR operator (`|`), each bit of the result is 1 if there is at least one 1 at the corresponding position in operands, and 0 if both bits in the operands are 0

```
a          1 0 1 0 0 1 0 0
b          1 0 0 0 0 1 1 0
a | b      1 0 1 0 0 1 1 0
```

The bit-wise XOR operator (`^`), sets a bit of the result to 1 if bits at the corresponding position in operands are different, and to 0 if they are the same

```
a        1 0 1 0 0 1 0 0
b        1 0 0 0 0 1 1 0
a ^ b    0 0 1 0 0 0 1 0
```

As can be expected, negating operator (`~`) just reverses (flips) the bits

```
a        1 0 1 0 0 1 0 0
~a       0 1 0 1 1 0 1 1
```

Let us notice here, that XORing has an interesting and useful feature. Let us see the result of XORing a bit sequence a with all ones:

```
a        1 0 1 0 0 1 0 0
b        1 1 1 1 1 1 1 1
a ^ b    0 1 0 1 1 0 1 1
```

We see that XORing the value a with all ones gives negation of a — wherever there was 1 in a, we get 0, and _vice versa._

Now let us try to XOR our a with all zeros:

```
a        1 0 1 0 0 1 0 0
b        0 0 0 0 0 0 0 0
a ^ b    1 0 1 0 0 1 0 0
```

This time what we got is exactly the same as a! So, XORing a bit with 1 flips its value, XORing it with zero – reproduces the same value.

## Listing 8 BAA-Bits/Bits.java

```java
public class Bits {
    public static void main (String[] args) {
        int a = 0b11111111;   // 255 or 0xFF
        System.out.println("a = " + a);
        int b = 0x7F;         // 127
        System.out.println("b = " + b);

        a = 3; // 00...011
        System.out.println(a + " " + (a << 1) + " " +
                          (a << 2) + " " + (a << 3));
        a = -1;
        int firstByte  = a & 255;
        int secondByte = (a >> 8) & 0xFF;
        System.out.println("-1: " + secondByte + " " +
                                    firstByte);
        a = 0b1001;
        b = 0b0101;
        System.out.println("AND: " + (a & b) + "; " +
                            "OR: " + (a | b) + "; " +
                           "XOR: " + (a ^ b) + "; " +
                           " ~a: " + (~a)    + "; " +
                           " ~b: " + (~b));
    }
}
```
