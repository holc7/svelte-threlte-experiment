
<script>
  import { Group } from 'three'
  import { T, forwardEventHandlers } from '@threlte/core'
  import { useGltf } from '@threlte/extras'

  export const ref = new Group()

  const gltf = useGltf('/2017_audi_s5-transformed.glb', { useDraco: true })

  const component = forwardEventHandlers()
</script>

<T is={ref} dispose={false} {...$$restProps} bind:this={$component}>
  {#await gltf}
    <slot name="fallback" />
  {:then gltf}
    <T.Group rotation={[-Math.PI / 2, 0, 0]}>
      <T.Mesh geometry={gltf.nodes.Object_6.geometry} material={gltf.materials['11Mtl']} />
      <T.Mesh geometry={gltf.nodes.Object_8.geometry} material={gltf.materials['12Mtl']} />
      <T.Mesh geometry={gltf.nodes.Object_10.geometry} material={gltf.materials.Caliper1Mtl} />
      <T.Mesh geometry={gltf.nodes.Object_12.geometry} material={gltf.materials.Dashsc1Mtl} />
      <T.Mesh geometry={gltf.nodes.Object_14.geometry} material={gltf.materials.Drl5Mtl} />
      <T.Mesh geometry={gltf.nodes.Object_16.geometry} material={gltf.materials.Meshesbadges1Mtl} />
      <T.Mesh geometry={gltf.nodes.Object_18.geometry} material={gltf.materials.Mesheschassis11Mtl} />
      <T.Mesh geometry={gltf.nodes.Object_20.geometry} material={gltf.materials.Meshesengine1Mtl} />
      <T.Mesh geometry={gltf.nodes.Object_22.geometry} material={gltf.materials.Meshesglass61Mtl} />
      <T.Mesh geometry={gltf.nodes.Object_24.geometry} material={gltf.materials.MeshesglassClear0011Mtl} />
      <T.Mesh geometry={gltf.nodes.Object_26.geometry} material={gltf.materials.MeshesglassRed61Mtl} />
      <T.Mesh geometry={gltf.nodes.Object_28.geometry} material={gltf.materials.MeshesglassRed71Mtl} />
      <T.Mesh geometry={gltf.nodes.Object_30.geometry} material={gltf.materials.Meshesinterior11Mtl} />
      <T.Mesh geometry={gltf.nodes.Object_32.geometry} material={gltf.materials.Mesheschassis11Mtl} />
      <T.Mesh geometry={gltf.nodes.Object_34.geometry} material={gltf.materials.Mesheslights00561Mtl} />
      <T.Mesh geometry={gltf.nodes.Object_36.geometry} material={gltf.materials.Mesheslights141Mtl} />
      <T.Mesh geometry={gltf.nodes.Object_38.geometry} material={gltf.materials.Meshespaint131Mtl} />
      <T.Mesh geometry={gltf.nodes.Object_40.geometry} material={gltf.materials.Meshespaint141Mtl} />
      <T.Mesh geometry={gltf.nodes.Object_42.geometry} material={gltf.materials.Meshpart1Mtl} />
      <T.Mesh geometry={gltf.nodes.Object_44.geometry} material={gltf.materials.Meshpart2Mtl} />
      <T.Mesh geometry={gltf.nodes.Object_46.geometry} material={gltf.materials.Plate1Mtl} />
      <T.Mesh geometry={gltf.nodes.Object_48.geometry} material={gltf.materials.Reflector1Mtl} />
      <T.Mesh geometry={gltf.nodes.Object_50.geometry} material={gltf.materials.Remote1Mtl} />
      <T.Mesh geometry={gltf.nodes.Object_52.geometry} material={gltf.materials.Rotor1Mtl} />
      <T.Mesh geometry={gltf.nodes.Object_54.geometry} material={gltf.materials.Rv2Mtl} />
      <T.Mesh geometry={gltf.nodes.Object_56.geometry} material={gltf.materials.Tire1Mtl} />
    </T.Group>
  {:catch error}
    <slot name="error" {error} />
  {/await}

  <slot {ref} />
</T>
