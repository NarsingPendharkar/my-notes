Here are clean, structured Markdown notes following your requested format 👇


---

1. Copy by Value (Pass by Value)

Description

Copy by value means a copy of the actual data is passed, not the original reference.
Changes made to the copied variable do NOT affect the original variable.

Example

int a = 10;
int b = a; // copy by value

b = 20;

System.out.println(a); // 10 (unchanged)
System.out.println(b); // 20

Key Points

Separate memory locations

Safe (no side effects)

Used for primitive types in Java



---

2. Copy by Reference

Description

Copy by reference means the reference (address) of the object is copied, not the actual object.
Both variables point to the same memory location, so changes affect both.

Example

class Person {
    String name;
}

Person p1 = new Person();
p1.name = "Narsing";

Person p2 = p1; // reference copy

p2.name = "Raj";

System.out.println(p1.name); // Raj (changed)
System.out.println(p2.name); // Raj

Key Points

Same memory location shared

Changes reflect in all references

Used for objects in Java



---

3. Shallow Copy

Description

Shallow copy creates a new object, but copies references of nested objects.
So, inner objects are still shared.

Example

class Address {
    String city;
}

class Person {
    String name;
    Address address;
}

Address addr = new Address();
addr.city = "Pune";

Person p1 = new Person();
p1.name = "Narsing";
p1.address = addr;

// Shallow copy
Person p2 = p1;

p2.address.city = "Mumbai";

System.out.println(p1.address.city); // Mumbai (affected)

Key Points

Outer object is new (sometimes), but inner objects are shared

Faster, less memory

Risk of unintended changes



---

4. Deep Copy

Description

Deep copy creates a completely independent copy, including all nested objects.
Changes in one object do NOT affect the other.

Example

class Address {
    String city;
}

class Person {
    String name;
    Address address;
}

Address addr = new Address();
addr.city = "Pune";

Person p1 = new Person();
p1.name = "Narsing";
p1.address = addr;

// Deep copy
Person p2 = new Person();
p2.name = p1.name;

Address newAddr = new Address();
newAddr.city = p1.address.city;
p2.address = newAddr;

p2.address.city = "Mumbai";

System.out.println(p1.address.city); // Pune (unchanged)
System.out.println(p2.address.city); // Mumbai

Key Points

Completely separate memory

No shared references

Safer but more memory & processing



---

🔥 Quick Comparison

Concept	Memory Sharing	Changes Affect Original	Used For

Copy by Value	❌ No	❌ No	Primitives
Copy by Reference	✅ Yes	✅ Yes	Objects
Shallow Copy	⚠️ Partial	⚠️ Yes (nested)	Fast copy
Deep Copy	❌ No	❌ No	Safe copy



---

If you want, I can give interview-ready tricky questions on these topics (very commonly asked for Java dev roles).