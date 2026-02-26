# WebGPU

- Level: L5
- Status: Emerging
- Depth: watchlist
- Specs:
  - WebGPU specification context
- Prerequisites: File System Access API
- Next Topics: L6 - Applied Systems

---

## 1. Official Term

WebGPU

## 2. Formal Definition

WebGPU adalah API grafis/komputasi modern
yang memberi akses lebih dekat ke kapabilitas GPU,
untuk rendering dan komputasi berperforma tinggi di web.

## 3. Mental Model

WebGPU memberi pipeline eksplisit (device, buffer, command encoder, queue)
yang lebih rendah level dibanding WebGL.

### Wireframe Ringkas

```text
requestAdapter -> requestDevice
   -> create buffers/pipeline
   -> encode commands
   -> submit to GPU queue
```

## 4. Runtime Perspective

- Thread/process: command recording biasanya dari context JS; eksekusi nyata terjadi di subsistem GPU.
- Queue model: command submission bersifat async terhadap jalur render utama.
- Scheduling: browser/driver mengatur eksekusi command queue ke hardware.
- Rendering interaction: workload GPU berat dapat memengaruhi frame timing keseluruhan.
- Dampak performa: potensi throughput tinggi, tapi setup pipeline kompleks.
- Dampak memori: resource GPU (textures/buffers) perlu lifecycle management ketat.
- Dampak keamanan: API didesain dengan sandboxing dan validasi untuk mitigasi risiko driver/hardware.

## 5. Why This Exists

Untuk memenuhi kebutuhan grafis dan komputasi modern di web
(me-render scene kompleks, compute workloads, dll) dengan kontrol lebih baik.

## 6. Minimal Code Example

```js
if (navigator.gpu) {
  const adapter = await navigator.gpu.requestAdapter();
  const device = await adapter.requestDevice();
  console.log("WebGPU ready", !!device);
}
```

## 7. Common Misconceptions

- "WebGPU adalah pengganti drop-in WebGL"
  - Koreksi: model API berbeda dan membutuhkan desain pipeline baru.
- "Kalau ada GPU pasti semua fitur sama"
  - Koreksi: capability tergantung browser, driver, dan hardware.

## 8. Pitfalls and Best Practices

- Pitfall: tidak merilis resource GPU saat tidak digunakan.
- Pitfall: overengineering pipeline untuk kasus sederhana.
- Best practice: mulai dari use case jelas, ukur bottleneck, lalu scale complexity.

## 9. Prerequisites

- [Rendering Pipeline](../L3-performance-and-security/rendering-pipeline.md)
- [Browser Process Model Deep Dive](../L4-advanced-deep-dive/browser-process-model-deep-dive.md)

## 10. Next Topics

- L6 - Applied Systems
