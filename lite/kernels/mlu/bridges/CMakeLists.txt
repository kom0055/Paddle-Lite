if(NOT LITE_WITH_MLU)
  return()
endif()

lite_cc_library(subgraph_bridge_utility_mlu SRCS utility.cc DEPS ${mlu_builder_libs} tensor)
lite_cc_library(subgraph_bridge_tensor_mlu SRCS tensor.cc DEPS ${mlu_builder_libs})
lite_cc_library(subgraph_bridge_graph_mlu SRCS graph.cc DEPS subgraph_bridge_utility_mlu subgraph_bridge_tensor_mlu)

set(mlu_subgraph_bridge_deps subgraph_bridge_registry subgraph_bridge_engine subgraph_bridge_utility_mlu subgraph_bridge_graph_mlu)

lite_cc_library(subgraph_bridge_act_op_mlu SRCS act_op.cc DEPS ${mlu_subgraph_bridge_deps})
lite_cc_library(subgraph_bridge_batch_norm_op_mlu SRCS batch_norm_op.cc DEPS ${mlu_subgraph_bridge_deps})
lite_cc_library(subgraph_bridge_conv_op_mlu SRCS conv_op.cc DEPS ${mlu_subgraph_bridge_deps})
lite_cc_library(subgraph_bridge_elementwise_ops_mlu SRCS elementwise_ops.cc DEPS ${mlu_subgraph_bridge_deps})
lite_cc_library(subgraph_bridge_pool_op_mlu SRCS pool_op.cc DEPS ${subgraph_bridge_deps_mlu})
lite_cc_library(subgraph_bridge_softmax_op_mlu SRCS softmax_op.cc DEPS ${subgraph_bridge_deps_mlu})
lite_cc_library(subgraph_bridge_fc_op_mlu SRCS fc_op.cc DEPS ${subgraph_bridge_deps_mlu})
set(mlu_subgraph_bridges
        subgraph_bridge_registry
        subgraph_bridge_utility_mlu
        subgraph_bridge_graph_mlu
        subgraph_bridge_act_op_mlu
        subgraph_bridge_conv_op_mlu
        subgraph_bridge_elementwise_ops_mlu
        subgraph_bridge_pool_op_mlu
        subgraph_bridge_softmax_op_mlu
        subgraph_bridge_fc_op_mlu
        subgraph_bridge_batch_norm_op_mlu
        CACHE INTERNAL "mlu_subgraph_bridges")


# lite_cc_library(subgraph_test_helper_mlu SRCS test_helper.cc DEPS ${mlu_subgraph_bridges})
# lite_cc_test(test_conv_converter_mlu SRCS conv_op_test.cc DEPS scope optimizer target_wrapper_host model_parser program ${mlu_subgraph_bridges} subgraph_compute_mlu subgraph_test_helper_mlu)
# lite_cc_test(test_act_converter_mlu SRCS act_op_test.cc DEPS scope optimizer target_wrapper_host model_parser program ${mlu_subgraph_bridges} subgraph_compute_mlu subgraph_test_helper_mlu)
# lite_cc_test(test_batch_norm_converter_mlu SRCS batch_norm_op_test.cc DEPS scope optimizer target_wrapper_host model_parser program ${mlu_subgraph_bridges} subgraph_compute_mlu subgraph_test_helper_mlu)
# lite_cc_test(test_elementwise_converter_mlu SRCS elementwise_ops_test.cc DEPS scope optimizer target_wrapper_host model_parser program ${mlu_subgraph_bridges} subgraph_compute_mlu subgraph_test_helper_mlu)
# lite_cc_test(test_pool_converter_mlu SRCS pool_op_test.cc DEPS scope optimizer target_wrapper_host model_parser program ${mlu_subgraph_bridges} subgraph_compute_mlu subgraph_test_helper_mlu)
# lite_cc_test(test_softmax_converter_mlu SRCS softmax_op_test.cc DEPS scope optimizer target_wrapper_host model_parser program ${mlu_subgraph_bridges} subgraph_compute_mlu subgraph_test_helper_mlu)
# lite_cc_test(test_fc_converter_mlu SRCS fc_op_test.cc DEPS scope optimizer target_wrapper_host model_parser program ${mlu_subgraph_bridges} subgraph_compute_mlu subgraph_test_helper_mlu)

message(STATUS "+++++ mlu_subgraph_bridges: ${mlu_subgraph_bridges}")
