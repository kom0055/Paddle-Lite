if(NOT LITE_WITH_XPU)
  return()
endif()

if(LITE_WITH_XTCL)
  add_subdirectory(bridges)
  add_kernel(subgraph_compute_xpu XPU basic SRCS subgraph_compute.cc DEPS ${lite_kernel_deps} device_xpu subgraph_bridge_engine ${xpu_subgraph_bridges})
else()
  add_kernel(conv_compute_xpu XPU basic SRCS conv_compute.cc DEPS ${lite_kernel_deps})
  add_kernel(io_copy_compute_xpu XPU basic SRCS io_copy_compute.cc DEPS ${lite_kernel_deps} target_wrapper_xpu)
  add_kernel(batch_norm_compute_xpu XPU basic SRCS batch_norm_compute.cc DEPS ${lite_kernel_deps})
  add_kernel(activation_compute_xpu XPU basic SRCS activation_compute.cc DEPS ${lite_kernel_deps})
  add_kernel(pool_compute_xpu XPU basic SRCS pool_compute.cc DEPS ${lite_kernel_deps})
  add_kernel(elementwise_compute_xpu XPU basic SRCS elementwise_compute.cc DEPS ${lite_kernel_deps})
  add_kernel(mul_compute_xpu XPU basic SRCS mul_compute.cc DEPS ${lite_kernel_deps})
  add_kernel(softmax_compute_xpu XPU basic SRCS softmax_compute.cc DEPS ${lite_kernel_deps})
  add_kernel(scale_compute_xpu XPU basic SRCS scale_compute.cc DEPS ${lite_kernel_deps})
  add_kernel(lookup_table_compute_xpu XPU basic SRCS lookup_table_compute.cc DEPS ${lite_kernel_deps})
  add_kernel(layer_norm_compute_xpu XPU basic SRCS layer_norm_compute.cc DEPS ${lite_kernel_deps})
  add_kernel(dropout_compute_xpu XPU basic SRCS dropout_compute.cc DEPS ${lite_kernel_deps})
  add_kernel(matmul_compute_xpu XPU basic SRCS matmul_compute.cc DEPS ${lite_kernel_deps})
  add_kernel(stack_compute_xpu XPU basic SRCS stack_compute.cc DEPS ${lite_kernel_deps})
  add_kernel(slice_compute_xpu XPU basic SRCS slice_compute.cc DEPS ${lite_kernel_deps})
  add_kernel(cast_compute_xpu XPU basic SRCS cast_compute.cc DEPS ${lite_kernel_deps})
  add_kernel(__xpu__resnet50_compute_xpu XPU extra SRCS __xpu__resnet50_compute.cc DEPS ${lite_kernel_deps})
  add_kernel(__xpu__multi_encoder_compute_xpu XPU extra SRCS __xpu__multi_encoder_compute.cc DEPS ${lite_kernel_deps})
endif()
