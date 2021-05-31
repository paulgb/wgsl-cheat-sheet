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

### Vectors and Matrices

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
