# Tugas-Menggambar-WebGL-GRAFKOM-D-2024

Nama  | NRP
------------- | -------------
Azhar Abiyu Rasendriya H  | 5025211177

Tugas ini adalah menampilkan objek 3D berbasis WebGL yang mendemonstrasikan rendering, efek cahaya, dan animasi untuk objek 3D. Tugas ini diimplementasikan menggunakan HTML, JavaScript, dan WebGL API. Untuk objek atau model yang akan buat adalah pil yang biasanya digunakan obat.

Github Repo : https://github.com/pusendut/Tugas-Menggambar-WebGL-GRAFKOM-D-2024

Github IO   : https://tugas-menggambar-web-gl-grafkom-d-2024.vercel.app/ (Github page sudah saya coba berkali-kali tetapi masih gagal deploy)

## Gambaran Kode

### Vertex Shader
```glsl
attribute vec4 a_position;
attribute vec3 a_normal;

uniform mat4 u_projection;
uniform mat4 u_view;
uniform mat4 u_world;

varying vec3 v_normal;

void main() {
  gl_Position = u_projection * u_view * u_world * a_position;
  v_normal = mat3(u_world) * a_normal;
}
```

### Fragment Shader
```glsl
precision mediump float;

varying vec3 v_normal;

uniform vec4 u_diffuse;
uniform vec3 u_lightDirection;

void main() {
  vec3 normal = normalize(v_normal);
  float light = max(dot(u_lightDirection, normal), 0.0);
  gl_FragColor = vec4(u_diffuse.rgb * light, u_diffuse.a);
}
```

### Rotasi Pada Objek
```javascript
let rotation = 0;
function render() {
  rotation += 0.01;

  const worldMatrix = m4.yRotation(rotation);
  gl.uniformMatrix4fv(u_world, false, worldMatrix);

  gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);
  gl.drawArrays(gl.TRIANGLE_STRIP, 0, positions.length / 3);

  requestAnimationFrame(render);
}
render();
```

## Dependensi
- [WebGL Fundamentals](https://webglfundamentals.org)

## Dokumentasi

### Modeling object menggunakan blender
![image](https://github.com/user-attachments/assets/45c51d2f-8132-4d7c-867f-99ef373ac57d)

### Shading Object menggunakan blender (tidak diimplementasikan pada Github IO)
![image](https://github.com/user-attachments/assets/bad5a32a-a5c0-4924-8b9a-ae898752e113)

### Pengetesan GLB file pada web https://gltf-viewer.donmccurdy.com/ (tidak diimplementasikan pada Github IO)
![image](https://github.com/user-attachments/assets/e1f0636e-46c1-4d2f-a733-6440518b2e9f)

### Implementasi HTML dan Javascript untuk rendering model menggunakan WebGL melalui live server VScode
![image](https://github.com/user-attachments/assets/b896afa8-5674-48ab-8207-9fe0ecb90021)



