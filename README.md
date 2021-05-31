# WGSL Cheat Sheet

This is a reference to WGSL syntax for users coming from GLSL. It is not meant to be complete, but to cover some common usages.

WGSL is still evolving, so some things may change before the final version. This reference is based on the [WGSL draft spec](https://www.w3.org/TR/WGSL/).

## Types

### Primitives

<table>
  <tr>
    <th>WGSL</th>
    <th>GLSL</th>
    <th>Note</th>
  </tr>
  <tr>
    <td><samp>bool</samp></td>
    <td><samp>bool</samp></td>
    <td><samp>true</samp> or <samp>false</samp></td>
  </tr>
  <tr>
    <td><samp>i32</samp></td>
    <td><samp>int</samp></td>
    <td>32-bit signed integer</td>
  </tr>
  <tr>
    <td><samp>u32</samp></td>
    <td><samp>uint</samp></td>
    <td>32-bit unsigned integer</td>
  </tr>
  <tr>
    <td><samp>f32</samp></td>
    <td><samp>float</samp></td>
    <td>Single-precision float</td>
  </tr>
  <tr>
    <td><em>Not available</em></td>
    <td><samp>double</samp></td>
    <td>Double-precision float</td>
  </tr>
</table>

### Composite Types

<table>
  <tr>
    <th>WGSL</th>
    <th>GLSL</th>
    <th>Note</th>
  </tr>
  <tr>
    <td><samp>vec<em>N</em>&lt;bool&gt;</samp></td>
    <td><samp>bvec<em>N</em></samp></td>
    <td>Vector of <em>N</em> ∈ {2, 3, 4} bools.</td>
  </tr>
  <tr>
    <td><samp>vec<em>N</em>&lt;i32&gt;</samp></td>
    <td><samp>ivec<em>N</em></samp></td>
    <td>Vector of <em>N</em> ∈ {2, 3, 4} signed integers.</td>
  </tr>
  <tr>
    <td><samp>vec<em>N</em>&lt;u32&gt;</samp></td>
    <td><samp>uvec<em>N</em></samp></td>
    <td>Vector of <em>N</em> ∈ {2, 3, 4} unsigned integers.</td>
  </tr>
  <tr>
    <td><samp>vec<em>N</em>&lt;f32&gt;</samp></td>
    <td><samp>vec<em>N</em></samp></td>
    <td>Vector of <em>N</em> ∈ {2, 3, 4} floats.</td>
  </tr>
  <tr>
    <td><em>Not available</em></td>
    <td><samp>dvec<em>N</em></samp></td>
    <td>Vector of <em>N</em> ∈ {2, 3, 4} double-precision vectors.</td>
  </tr>
  <tr>
    <td><samp>mat<em>N</em>x<em>M</em>&lt;f32&gt;</samp></td>
    <td><samp>mat<em>N</em>x<em>M</em></samp>, <samp>mat<em>N</em></samp></td>
    <td>Matrix of <em>NxM</em> ∈ {2, 3, 4} columns and rows (or <em>NxN</em>).</td>
  </tr>
</table>

## Variables

<table>
  <tr>
    <th>WGSL</th>
    <th>GLSL</th>
    <th>Note</th>
  </tr>
  <tr>
    <td><samp>var m: i32 = 4;</samp></td>
    <td><samp>int m = 4;</samp></td>
    <td><em>var</em> creates a local variable.</td>
  </tr>
  <tr>
    <td><samp>let m: i32 = 4;</samp></td>
    <td><em>Not available?</em></td>
    <td><em>let</em> creates an immutable binding.</td>
  </tr>
</table>

## Literals

<table>
  <tr>
    <th>WGSL</th>
    <th>GLSL</th>
    <th>Note</th>
  </tr>
  <tr>
    <td><samp>123</samp></td>
    <td><samp>123</samp> (when used in <samp>int</samp> context)</td>
    <td></td>
  </tr>
  <tr>
    <td><samp>123u</samp>, <samp>123u32</samp></td>
    <td><samp>123</samp> (when used in <samp>uint</samp> context)</td>
    <td>WGSL does not infer int type from context; you need to be explicit.</td>
  </tr>
</table>

## `switch` syntax

WGSL needs explicit `fallthrough` to not `break` at the end of a switch block. `my_var` must be a `u32` (I think?).

<table>
  <tr>
    <th>WGSL</th>
    <th>GLSL</th>
  </tr>
  <tr>
    <td>
<pre>
switch (my_var) {
  case 0: {
    fallthrough;
  }
  case 1: {
    foo = 1;
  }
  case 2: {
    foo = 4;
  }
}
</pre>
    </td>
    <td><pre>
switch (my_var) {
  case 0:
  case 1:
    foo = 1;
    break;
  case 2:
    foo = 4;
}
</pre></td>
  </tr>
</table>

## Shader Function Structure

### Vertex Shader

<table>
  <tr>
    <th>WGSL</th>
    <th>GLSL</th>
  </tr>
  <tr>
    <td>
<pre>
// Structure of vertex shader output
struct VertexOutput {
&#9;[[builtin(position)]] position: vec4&lt;f32&gt;;
&#9;[[location(0)]] baz;
};
&#9;
// Vertex shader function
[[stage(vertex)]]
fn vs_main(
&#9;[[location(0)]] foo: vec2&lt;f32&gt;,
&#9;[[location(1)]] bar: vec4&lt;f32&gt;,
) -&gt; VertexOutput {
&#9;var out: VertexOutput;
&#9;if (foo.x &gt; foo.y) {
&#9;&#9;discard;
&#9;}
&#9;out.baz = vec4&lt;f32&gt;(0.0, 1.0, 0.0, 1.0);
&#9;out.position = bar;
&#9;return out;
}
</pre>
    </td>
    <td><pre>
// Inputs from vertex buffer.
layout(location=0) in vec2 foo;
layout(location=1) in vec4 bar;

// Output to frag shader.
layout(location=0) out vec4 baz;

void main() {
&#9;if (foo.x &gt; foo.y) {
&#9;&#9;discard;
&#9;}
&#9;baz = vec4(0.0, 1.0, 0.0, 1.0);
&#9;gl_Position = bar;
}
</pre></td>
  </tr>
</table>
